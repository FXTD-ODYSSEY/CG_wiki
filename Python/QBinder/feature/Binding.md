# 绑定变量

> &emsp;&emsp;绑定变量 是 绑定容器 Binder 承载的变量类型
> &emsp;&emsp;默认直接赋值都会自动转换为 Binding 对象。

## Binding 变量绑定类

```Python
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

```Python
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

## FnBinding 函数绑定类

```Python
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


```Python
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
