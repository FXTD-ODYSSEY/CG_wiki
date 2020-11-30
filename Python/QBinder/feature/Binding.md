# 绑定变量

> &emsp;&emsp;绑定变量 是 绑定容器 Binder 承载的变量类型      
> &emsp;&emsp;默认直接赋值都会自动转换为 Binding 对象。

## Binding 变量绑定类

```python
from __future__ import print_function

# NOTE ctrl+c 暂停程序
import signal
signal.signal(signal.SIGINT, signal.SIG_DFL)

from Qt import QtWidgets
from QBinder import Binder

app = QtWidgets.QApplication([])


state = Binder()
state.text = "text"

# NOTE 通过字典获取 Binding 实例
binding = state["text"]

# NOTE Binding 支持 Signal API | 可以注册函数 当数值发生变化的时候出发函数
binding.connect(lambda:print('change value %s' % state.text))

state.text = "QBinder"
# NOTE 打印 `change value QBinder`

# NOTE 回调用到 Qt 事件队列的机制，需要启动 QApplication 才可以触发
app.exec_()

```

> &emsp;&emsp;binding 可以使用 connect 和 emit 方法来注册以及触发函数。

```python
from QBinder import Binder
state = Binder()
state.text = "text"

binding = state["text"]

# NOTE binding 有 get set 方法
print (binding.get())
# NOTE 打印 `text`
binding.set('QBinder')

print(state.text)
# NOTE 打印 `QBinder`
```

> &emsp;&emsp;使用 binding 的赋值语句比使用 set 方法要好，因为 set 方法只触发 QBinder 数据绑定的更新。
> &emsp;&emsp;赋值语句还会触发 model 的更新，因此不推荐是用 set 方法

## 数据双向绑定

```python
from __future__ import print_function

from Qt import QtWidgets
from QBinder import Binder

app = QtWidgets.QApplication([])


state = Binder()
state.text = "text"

edit = QtWidgets.QLineEdit()
# NOTE 直接添加单个参数情况会自动实现双向数据绑定
# NOTE 自动通过 textChanged 更新 state.text 的数据
edit.setText(lambda: state.text)

label = QtWidgets.QLabel()
# NOTE 因为 edit 修改自动更新 state.text 因此同时更新了 label 的绑定
label.setText(lambda: state.text)

widget = QtWidgets.QWidget()
layout = QtWidgets.QVBoxLayout()
widget.setLayout(layout)
layout.addWidget(edit)
layout.addWidget(label)

widget.show()

app.exec_()
```

> &emsp;&emsp;双向数据绑定是借助 Qt 的 meta 机制实现的。
> &emsp;&emsp;具体囊括的函数可以参照这个 [链接](https://github.com/FXTD-ODYSSEY/QBinder/blob/e6478b3e27e1655463ef2415d5a8c747d222c9f9/research/test_qt_meta.json)
> &emsp;&emsp;json 里面包含 updater 的部分就是支持双向数据绑定。

> &emsp;&emsp;如果不想双向数据绑定的话，可以改为 `edit.setText(lambda: state.text * 1)` 的方法，只要有运算就不会自动双向绑定了。

## FnBinding 函数绑定类

```python
from QBinder import Binder , FnBinding

state = Binder()

state.callback = FnBinding()
state.callback2 = FnBinding()

# NOTE 绑定函数
@state.callback
def test():
    print('FnBinding call')

state.callback()
# NOTE 打印 `FnBinding call`

class Test(object):

    # NOTE 绑定类函数
    @state.callback2
    def test(self,arg):
        print('test : ',arg)

inst = Test()

# NOTE 调用需要传入类实例
state.callback2(inst,"callback2")
# NOTE 类实例可以通过 字典的方式传入 信号槽连接
state.callback2[inst]("callback2")

```

## 继承 BinderTemplate 预设Binder


```python
from QBinder import BinderTemplate

class Template(BinderTemplate):
    text = "text"

    def __init__(self):
        # NOTE self 是 Binder 类实例化的对象
        self.num = 1

    def test(self):
        print("run callback")

# NOTE state 得到的 Binder 类实例化的对象
state = Template()

state.test()
# NOTE 打印 `run callback`
print(state.text)
# NOTE 打印 `text`
print(state.num)
# NOTE 打印 `1`
print(type(state["text"]))
# NOTE 打印 `<class 'QBinder.binding.Binding'>`
print(type(state["num"]))
# NOTE 打印 `<class 'QBinder.binding.Binding'>`

```

> &emsp;&emsp;BinderTemplate 可以通过继承类来预设 Binder 的属性数据。
