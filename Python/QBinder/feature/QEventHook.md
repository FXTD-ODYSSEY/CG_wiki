# QEventHook 事件钩子

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

![model 案例](//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/Python/QBinder/_img/feature/event_hook.gif)

> &emsp;&emsp;上面的案例结合 handler 和 QEventHook 可以实现更加灵活方便的组件写法。     
> &emsp;&emsp;handler 的使用场景是通过 >> 运算符重载对 binding 进行操作。     
> &emsp;&emsp;上面使用 Set 方法类就是用来解决 lambda 无法赋值的兼容方案。     
> &emsp;&emsp;简单的数据操作就不需要声明冗余的函数     

> &emsp;&emsp;QEventHook 会劫持 Qt 全局的事件响应，这样不需要继承组件来实现。     
> &emsp;&emsp;可以通过我的 劫持 钩子来直接扩展组件的行为响应。     
> &emsp;&emsp;QEventHook 使用单例模式，无论在哪里实例化都只获取同一个实例。(避免多重劫持导致性能下降)     

> &emsp;&emsp;QEventHook 支持两种写法 `add_hook` 或者 `>> 运算符` 。     
> &emsp;&emsp;>> 运算符重载的写法更加简洁，只是如果前面的组件有重载 \_\_rshift__ 运算符会导致出错。     
> &emsp;&emsp;事件绑定上支持 QEvent 和 字符串 两种写法。     

> &emsp;&emsp;支持的事件参考 Qt QEvent 文档 [链接](https://doc.qt.io/qtforpython/PySide2/QtCore/QEvent.html#PySide2.QtCore.PySide2.QtCore.QEvent.Type)
