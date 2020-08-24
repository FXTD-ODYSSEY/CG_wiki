# Socket 自动化添加工具

> &emsp;&emsp;这个工具可以根据配置文档批量在骨骼上添加 socket    
> &emsp;&emsp;由于 Unreal Python 插件并没有添加 socket 的功能    
> &emsp;&emsp;这里我通过 C++ 开发蓝图扩展了这部分的功能    

> + delete_skeletal_mesh_socket    
> + add_skeletal_mesh_socket    
> + get_skeleton_bone_num    
> + get_skeleton_bone_name    

![警告](//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/anim/02/00.png)

## 工具开启

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/anim/02/01.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

## 添加数据 生成 socket

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/anim/02/02.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

> &emsp;&emsp;右键添加一行数据，可以添加一行空数据    
> &emsp;&emsp;然后选择 Skeletal Mesh 点击 自动生成Socket 即可添加配置的 socket    
> &emsp;&emsp;点击清空 Socket 会将当前角色所有的 Socket 删除    

## 读取 CSV 数据

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/anim/02/03.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

> &emsp;&emsp;可以通过 Excel 软件编辑输出 csv 文件    
> &emsp;&emsp;然后通过工具读取 csv 文件    

## 修改并输出 csv 数据

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/anim/02/04.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

> &emsp;&emsp;可以通过双击插槽栏修改插槽的名称    
> &emsp;&emsp;生成插槽的时候名称也会随之变化。    
> &emsp;&emsp;编辑完成之后可以将数据导出为 csv 文件继续通过 Excel 进行修改    

## 骨骼找不到弹窗警告

![警告](//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/anim/02/05.png)

> &emsp;&emsp;如果角色上没有匹配的骨骼名称就会太过骨骼并且最后弹出警告。    

## 自定记录上次打开的 csv 文件进行读取

> &emsp;&emsp;每次开启工具都会读取上次打开的 csv 文件，除非路径的文件不存在。    
