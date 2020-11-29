# 绑定变量 handler

> &emsp;&emsp;handler 用来扩展 binding 的操作，简化代码复杂度。

## Set 

```Python
from QBinder import Binder
from QBinder.handler import Set

state = Binder()
state.text = "text"

state.text >> Set("change")

print(state.text)
# NOTE 打印 `change`
```

> &emsp;&emsp;通过运算符重载设置 Binding 值，用来解决 lambda 不支持赋值语句的问题。

```Python
from QBinder import Binder
from QBinder.handler import Set
from Qt import QtWidgets

app = QtWidgets.QApplication([])

container = QtWidgets.QWidget()
layout = QtWidgets.QVBoxLayout()
container.setLayout(layout)

edit = QtWidgets.QLineEdit()
label = QtWidgets.QLabel()

# NOTE 使用 Set 解决赋值问题
edit.textChanged.connect(lambda text: state.text >> Set(text))
label.setText(lambda: state.text)

layout.addWidget(edit)
layout.addWidget(label)
container.show()
app.exec_()
```

![handler_set 案例](//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/Python/QBinder/_img/feature/handler_set.gif)

> &emsp;&emsp;通过上面的写法可以手动实现双向绑定的效果。


## GroupBoxBind 

```Python
# 省略代码...
# NOTE self.StateGroup 为 QGroupBox
gstate.selected >> GroupBoxBind(self.StateGroup)
```

> &emsp;&emsp;绑定 QGroupBox 下的 RadioButton 勾选的 checkbox ，将 checkbox 的名称传递到 selected 变量里。 [参考 Todo 案例](/advance/todo.md)

## ItemConstructor 

> &emsp;&emsp;ItemConstructor 用来将 列表字典配置 数据转换为组件的构造函数 

```Python
gstate.todo_data = [
    {"text": "todo1", "completed": False},
    {"text": "todo2", "completed": True},
] * 5

# 省略代码...

class TodoItem(QtWidgets.QWidget, Ui_TodoItem):

    state = Binder()

    @inject(state)
    def __init__(self):
        super(TodoItem, self).__init__()
        dumper = self.state('dumper')
        dumper.set_auto_load(False)

        # NOTE gstate.todo_data 对应 组件 state 的数据
        self.state.text = ""
        self.state.completed = False

# 省略代码...

# NOTE 过滤函数配置 data 传入 gstate.todo_data 的数据 | 自动配置的组件的 visible 属性
filters = {
    "All": lambda data: data,
    "Active": lambda data: [d for d in data if not d["completed"]],
    "Completed": lambda data: [d for d in data if d["completed"]],
}

# NOTE ItemConstructor 用字典方法接受 组件类 然后需要传入 __layout__ 和 __binder__ 参数来完成构建， __filters__ 需要用到过滤则添加
# NOTE __layout__ 传入 QLayout 作为 组件的布局容器
# NOTE __binder__ 传入绑定容器的名称实现 todo_data 的数据匹配
gstate.todo_data >> ItemConstructor[TodoItem](
    __layout__=self.TodoList.layout(),
    __binder__="state",
    __filters__=lambda data: filters[gstate.selected](data),
)
```

> &emsp;&emsp;这个使用案例 [参考 Todo 案例](/advance/todo.md)

