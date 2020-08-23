
# 批量改名工具

> &emsp;&emsp;最近看了个[教程](https://www.bilibili.com/video/BV1bT4y177v8)，有相关重命名和匹配的操作。     
> &emsp;&emsp;于是就将功能通过 PySide 全部整合到一起了~    

![界面](//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/msic/02/01.png)

## 启动插件

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/msic/02/02.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

> &emsp;&emsp;默认不会拉开左侧的选项配置界面。    
> &emsp;&emsp;避免把美术人员吓着了，所以我将初始界面设计得比较简单。    

## 基础替换演示

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/msic/02/04.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>


> &emsp;&emsp;添加当前选择的物体。    
> &emsp;&emsp;查找关键字进行替换，关键字匹配的部分会用紫色背景高亮显示。    
> &emsp;&emsp;有了新名称之后也可以对名称单独进行修改实现独立命名    

## 图标说明

![图标说明](//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/msic/02/03.png)

> &emsp;&emsp;右键菜单也可以看到右侧图标对应的功能的说明    

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/msic/02/05.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

> &emsp;&emsp;功能基本上和右键菜单的说明对应    
> &emsp;&emsp;右键菜单最上面可以将菜单变为一个向窗口，方便多次点击。    

## 进阶配置案例 - 根据文件类型添加前缀

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/msic/02/06.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

> &emsp;&emsp;自动根据文件类型添加虚幻类型缩写    
> &emsp;&emsp;这个命名规则根据 github 的命名规范仓库来的 [地址](https://github.com/Allar/ue4-style-guide)    

![图标说明](//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/msic/02/07.png)

> &emsp;&emsp;可以在工具的帮助上找到链接    

> &emsp;&emsp;命名规则是通过类型匹配获取的，可以参考工具里的 [convention.json](https://github.com/FXTD-ODYSSEY/Unreal-PyToolkit/blob/master/Content/Msic/Renamer/convention.json)    
> &emsp;&emsp;部分类型我在 Python 找不到，前面加了 * 标识，还有一些如贴图加后缀的需要人为帮忙判断。    


## 进阶配置案例 - 正则表达式匹配

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/msic/02/08.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

> &emsp;&emsp;正则表达式通过特定标记符号规则实现复杂名称的匹配    
> &emsp;&emsp;用好正则可以极大简化各种复杂的重命名操作 [正则表达式讲解](https://www.runoob.com/regexp/regexp-syntax.html)    

## 进阶配置案例 - 前缀添加序号

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/msic/02/09.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

> &emsp;&emsp;序号可以通过上下移动调整序号的号码    
> &emsp;&emsp;文件序号可以通过左侧选项面板进行调整。    

> &emsp;&emsp;下面的变量配置可以直接进行调用    
> &emsp;&emsp;会自动替换为记录的变量值    
> &emsp;&emsp;替换也可以使用变量值    

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/msic/02/10.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

