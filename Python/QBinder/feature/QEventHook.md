# QEventHook 事件钩子

> &emsp;&emsp;QEventHook 的目的是跳过重载 类的 事件方法实现普通组件的特殊事件回调。

> &emsp;&emsp;比如说我们想让 Label 鼠标 Hover 状态下改变颜色。
> &emsp;&emsp;传统方法需要写一个新的类，然后重载 QLabel 所继承的 QWidget enterEvent 实现相关的方法。
> &emsp;&emsp;但是重新构建一个新的类很麻烦，特别是结合 Qt Designer 开发就很不方便。

> &emsp;&emsp;因此我利用 Qt 的 全局 eventFilter 实现全局 event 过滤。
> &emsp;&emsp;QEventHook 会劫持 Qt 全局的事件响应，这样不需要继承新类来实现这些特定事件。     

## 使用案例

```python
from QBinder import Binder,QEventHook
from QBinder.handler import Set

from Qt import QtWidgets
from Qt import QtCore
from Qt import QtGui

# NOTE event_hook 使用单例模式
event_hook = QEventHook()

class WidgetTest(QtWidgets.QWidget):
    state = Binder()
    state.text = "text"
    state.num = 1
    state.color = "black"
    state.spin_color = "black"

    def __init__(self):
        super(WidgetTest, self).__init__()
        self.initialize()

    def initialize(self):
        layout = QtWidgets.QVBoxLayout()
        self.setLayout(layout)

        self.edit = QtWidgets.QLineEdit()
        self.label = QtWidgets.QLabel()
        layout.addWidget(self.edit)
        layout.addWidget(self.label)

        self.button.clicked.connect(lambda:self.state.text >> Set("asd"))
        self.edit.setText(lambda: self.state.text)
        self.label.setText(lambda: "message is %s" % self.state.text)
        
        event_hook.add_hook(self.edit,QtCore.QEvent.FocusIn,lambda:self.state.color >> Set("red"))
        event_hook.add_hook(self.edit,QtCore.QEvent.FocusOut,lambda:self.state.color >> Set("black"))
        self.label.setStyleSheet(lambda:"color:%s" % self.state.color)

        self.spin = QtWidgets.QSpinBox(self)
        self.label = QtWidgets.QLabel()
        layout.addWidget(self.spin)
        layout.addWidget(self.label)
        self.spin.setValue(lambda: self.state.num)
        self.label.setText(lambda: "num is %s" % self.state.num)
        
        self.spin >> event_hook("HoverEnter",lambda:self.state.spin_color >> Set("pink"))
        self.spin >> event_hook("HoverLeave",lambda:self.state.spin_color >> Set("blue"))
        self.label.setStyleSheet(lambda:"color:%s" % self.state.spin_color)

if __name__ == "__main__":
    app = QtWidgets.QApplication([])
    widget = WidgetTest()
    widget.show()
    app.exec_()

```

![model 案例](https://cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/Python/QBinder/_img/feature/event_hook.gif)

> &emsp;&emsp;上面的案例结合 handler 和 QEventHook 可以实现更加灵活方便的组件写法。     
> &emsp;&emsp;handler 的使用场景是通过 >> 运算符重载对 binding 进行操作。     
> &emsp;&emsp;上面使用 Set 方法类就是用来解决 lambda 无法赋值的兼容方案。     
> &emsp;&emsp;简单的数据操作就不需要声明冗余的函数     

> &emsp;&emsp;QEventHook 使用单例模式，无论在哪里实例化都只获取同一个实例。(避免多重劫持导致性能下降)     

> &emsp;&emsp;QEventHook 支持两种写法 `add_hook` 或者 `>> 运算符` 。     
> &emsp;&emsp;>> 运算符重载的写法更加简洁，只是如果前面的组件有重载 \_\_rshift__ 运算符会导致出错。     
> &emsp;&emsp;事件绑定上支持 QEvent 和 字符串 两种写法。     

> &emsp;&emsp;支持的事件参考 Qt QEvent 文档 [链接](https://doc.qt.io/qtforpython/PySide2/QtCore/QEvent.html#PySide2.QtCore.PySide2.QtCore.QEvent.Type)

## 回调函数 参数自动填充

```Python
from QBinder import QEventHook

from Qt import QtWidgets
from Qt import QtCore
from Qt import QtGui

event_hook = QEventHook()

app = QtWidgets.QApplication([])

label = QtWidgets.QLabel("display")
label.show()

# NOTE 扩展 label 为可点击组件

# NOTE 可不接受参数或者接受 event 参数
label >> event_hook("MouseButtonPress",lambda:print("clicked"))
label >> event_hook("MouseButtonPress",lambda event:print("clicked",event))

app.exec_()
```

![model 案例](https://cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/Python/QBinder/_img/feature/event_hook2.gif)

> &emsp;&emsp;这里传入的 lambda 同时支持没有参数和一个参数。
> &emsp;&emsp;如果填入了一个参数，传入的是 hook 组件说接受到的 Event ，方便特定函数获取 event 的数据来进行特殊操作。

## 逆向事件过滤

```Python
from QBinder import QEventHook

from Qt import QtWidgets
from Qt import QtCore
from Qt import QtGui

event_hook = QEventHook()

app = QtWidgets.QApplication([])

label = QtWidgets.QLabel("display")
label.show()
modal = QtWidgets.QWidget()
modal.show()

# NOTE 点击外部组件隐藏窗口
modal >> ~event_hook("MouseButtonPress",lambda:modal.hide())

app.exec_()
```

> &emsp;&emsp;QEventHook 还提供了逆向事件过滤， 在实例对象前添加 ~ 运算符即可。
> &emsp;&emsp;也就是判断条件调整为除了 传入的组件意外的所有组件均进行触发。
> &emsp;&emsp;比如要做一个 Modal 模态窗口，可以点击外部任意区域来隐藏自身。 (更简单的方法是 setWindowFlag(QtCore.Qt.Popup) )

> 注意: 逆向事件过滤接受 `reciever` `event` 两个参数，按顺序传入。

## 注意事项

```Python
# ! 传入 Qt 事件会报错
modal >> event_hook("MouseButtonPress",modal.hide)
```

> &emsp;&emsp;为了判断函数可以传入的参数， hook 的回调函数 只支持 Python 函数 ， 不支持 Qt 函数传入。 传入会直接触发报错。

---

> &emsp;&emsp;文件拖拽支持需要注意 `dragEnterEvent` 和 `dragMoveEvent` 必须使用虚函数重载。
> &emsp;&emsp;利用 QEventHook 劫持不起作用，详情可以参考 [dragDropTest.py](https://github.com/FXTD-ODYSSEY/QBinder/blob/master/test/dragdropTest.py) 测试脚本。

