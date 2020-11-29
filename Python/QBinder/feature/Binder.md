
# 绑定容器

> &emsp;&emsp;Binder 是数据绑定的容器，一般用于组件。     
> &emsp;&emsp;GBinder 是单例模式容器，全局实例化都是同一个对象，更方便传递数据。

## 绑定变量

```python
from QBinder import Binder

state = Binder()
state.num = 1

print(type(state.num))
# <type 'int'>
print(type(state["num"]))
# <class 'QBinder.binding.Binding'>

```

> &emsp;&emsp;Binder 绑定变量声明只需要正常赋值即可。     
> &emsp;&emsp;赋值之后获取的是变量的值，但是背后存储的是 Binding 类型的实例。    
> &emsp;&emsp;可以通过 字典获取的方式获取背后真正的存储对象。

## 命令方法

```python
from QBinder import Binder

state = Binder()
dispatcher = state("dispatcher")
print(type(dispatcher))
# <class 'QBinder.binder.BinderDispatcher'>
dumper = state("dumper")
print(type(dumper))
# <class 'QBinder.binder.BinderDumper'>

# state("dispatcher") 等价于 dispatcher.dispatcher()
# state("dumper") 等价于 dispatcher.dumper()

```

> &emsp;&emsp;实例化的 Binder 可以传入参数调用方法。     
> &emsp;&emsp;为了避免和绑定变量的命名冲突，传入的字符串会自动调用 BinderDispatcher 实例里的方法

## BinderDumper 数据持久化

```python
from QBinder import Binder

state = Binder()
# NOTE 指定 dumper 存储绑定变量数据
# NOTE 下次启动的时候会自动从本地文件读取数据到绑定变量
with state("dumper") as dumper:
    state.text = "text"

# NOTE 数据修改会自动将数据存储到临时目录的 json 文件
state.text = "chagne"

# NOTE 获取存储的路径 路径名称根据脚本运行的路径和 Binder生成的次序生成的
print(dumper.path)
# C:\Users\XXXXXX\AppData\Local\Temp\QBinder\687f513e1d4ce70b0fb0cd12ff7ac38c.json

# NOTE dumper 支持绑定数据的导入导出
path = r"C:\test.json"
dumper.save(path)
dumper.load(path)
```

> &emsp;&emsp;目前只支持了 json 数据的导入导出，后续可以开放更多数据持久化存储的 API ，方便不同的需求。    
> &emsp;&emsp;dumper 也可以 json 配置导入导出，

## BinderDumper 禁用

```python
from QBinder import Binder

state = Binder()
dumper = state("dumper")
dumper.set_auto_dump(False)

```

> &emsp;&emsp;默认绑定变量如果有绑定双向数据绑定的会自动进行 dump 数据存储操作。     
> &emsp;&emsp;倘若不需要可以使用 `set_auto_dump` 将这个 dumper 的自动 dump 禁用。

```python
from QBinder import constant
constant.AUTO_DUMP = False
```

> &emsp;&emsp;也可以使用上面的代码全局禁用 auto_dump 效果。     
> &emsp;&emsp;auto_dump 不会屏蔽上面 with 语句特殊指定的 dump 。

