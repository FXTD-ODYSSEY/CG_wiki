# Qt MVC 兼容

## 使用 Model 类

```python
from QBinder import Binder, Model
from Qt import QtWidgets

state = Binder()

state.text = "text"
state.num_1 = "1"
state.num_2 = "2"
state.num_3 = "3"
state.num_4 = "4"

# NOTE 构建 QStandardItemModel
state.model = Model(
    [
        state["num_1"],
        state["num_2"],
        state["num_3"],
        state["num_4"],
    ]
)


app = QtWidgets.QApplication([])

combo = QtWidgets.QComboBox()
combo.setModel(state.model)

state.num_1 = "change_1"
state.num_2 = "change_2"

combo.show()

app.exec_()
```
![model 案例](//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/Python/QBinder/_img/feature/model.gif)

> &emsp;&emsp;通过 Model 可以构建 Qt 兼容的 Model ，同时 Binding 变化会触发 Model 的更新。

![model 案例](//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/Python/QBinder/_img/feature/model2.gif)

> &emsp;&emsp;上面是修改 model 同时同步多个 View 的效果。 [github链接](https://github.com/FXTD-ODYSSEY/QBinder/blob/master/test/modelTest.py)