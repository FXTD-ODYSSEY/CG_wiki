# Unreal-PyToolkit

> 嵌入 Python PySide 模块实现 Qt 界面开发    
> 说明文档链接 [wiki.l0v0.com/PyToolkit/](http://wiki.l0v0.com/PyToolkit/#/)

![工具集锦](//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/01.png)

> &emsp;&emsp;工具界面使用 PySide 组件库 [dayu_widgets](https://github.com/phenom-films/dayu_widgets)     
> &emsp;&emsp;插件在引擎版本 4.25.1 下运行没有问题。        

> &emsp;&emsp;使用本插件需要开启下列 Unreal 官方插件    
> + Python Editor Script Plugin     
> + Editor Scripting Utilities    
> + Sequencer Scripting    

> &emsp;&emsp;由于 Unreal Python 的官方插件是基于蓝图节点转换到 Python 调用的    
> &emsp;&emsp;所以不开启插件会导致相关的蓝图模块缺失，官方 Python 文档里面所提到的一些模块也将无法使用。    

## Python 库依赖

Content 目录下的 Python 目录默认会添加到 Python sys.path 里面   
Python 目录里面添加的依赖库如下:    
+ [PySide](https://pypi.org/project/PySide/) 
+ [FBX Python SDK](https://www.autodesk.com/developer-network/platform-technologies/fbx-sdk-2020-1)
+ [dayu_widgets](https://github.com/phenom-films/dayu_widgets)
+ [dayu_path](https://github.com/phenom-films/dayu_path)
+ [singledispatch](https://pypi.org/project/singledispatch/)
+ [Qt.py](https://github.com/mottosso/Qt.py)

> 附注： PySide 包整个有近 100M 大小，我全部上传到了 master 分支了，所以仓库会比较大，我预留了 码云 的仓库备份，方便用来加速。 [码云链接](https://gitee.com/ZSD_tim/Unreal-PyToolkit)    

