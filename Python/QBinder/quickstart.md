
# 快速开始

## QBinder 安装

> &emsp;&emsp;推荐使用 pip 安装 QBinder 包

```bash
pip install QBinder
```

> &emsp;&emsp;代码是纯 python 编写，兼容不同软件环境。     
> &emsp;&emsp;可以去 Github 链接获取最新的 release 版本，将 QBinder 文件夹拷贝到 Python 能够导入的目录里。


## 使用方法

```python
from QBinder import Binder
from Qt import QtWidgets

app = QtWidgets.QApplication([])
# NOTE 构建绑定容器和变量
binder = Binder()
binder.text = "text"

label = QtWidgets.QLabel()
# NOTE 不带绑定关系 - 单纯设置 label 的文本
label.setText(binder.text)

# NOTE 因为没有设置绑定关系，所以不会修改 label 的文本
binder.text = "change_1"

# NOTE 添加 lambda 将组件的方法关联绑定变量
# NOTE 同时也将 binder.text 的数据赋值到 label 上
label.setText(lambda:binder.text)

# NOTE 上面 lambda 关联了 setText 方法
# NOTE 当绑定变量更新的时候会自动触发 setText 方法将 label 的文本改为 change_2
binder.text = "change_2"

label.show()

app.exec_()
```

> &emsp;&emsp;QBinder 导入的时候会自动给 Qt 的特定方法注入 lambda 检测 ， 具体包括的方法可以参考 [hookconfig.py](https://github.com/FXTD-ODYSSEY/QBinder/blob/master/QBinder/hookconfig.py)     
> &emsp;&emsp;通过 lambda 函数配合绑定变量实现数据绑定。

> &emsp;&emsp;数据绑定可以简化组件的操作，将更多注意点放到数据上。


