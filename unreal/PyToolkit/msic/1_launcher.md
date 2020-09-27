## UE启动器

> &emsp;&emsp;这个工具使用来 C++ 触发快捷键实现 引擎 主界面的任意位置唤醒。    
> &emsp;&emsp;类似于 windows 上的启动器，我目前主要用来解决文件定位问题。    
> &emsp;&emsp;其实参考主流的启动器，玩法可以有很多，我并没有深入扩展。    

![界面](//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/unreal/PyToolkit/_img/msic/01/01.png)

<h2 style="text-align: center">

[启动器开发记录](https://blog.l0v0.com/posts/5905c2c9.html)
</h2>

## 启动插件

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/unreal/PyToolkit/_img/msic/01/02.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

> &emsp;&emsp;使用下拉菜单启动，或者使用在主窗口使用快捷键 Ctrl + F 唤起。    

![界面](//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/unreal/PyToolkit/_img/msic/01/03.png)

> &emsp;&emsp;快捷键可以在编辑器的首选项里面进行自定义设置。    

## 路径定位

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/unreal/PyToolkit/_img/msic/01/03.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

> &emsp;&emsp;定位器可以定位引擎的内部的相对路径以及系统内的绝对路径，粘贴路径到启动器然后按 Enter 进行定位。    
> &emsp;&emsp;定位器启动的时候会自动识别剪贴板的数据是否是合法路径，如果是合法路径会自动粘贴并保持全选状态。    
> &emsp;&emsp;复制系统文件路径可以按住 shift 右键菜单下有复制路径选项。    
> &emsp;&emsp;也可以安装 listary 之类的便捷工具，可以选择文件通过 ctrl+shift+c 复制路径。    
> &emsp;&emsp;有了定位器之后，多人协作可以直接发引擎的相对路径定位文件，不需要再发图片然后再一层层找路径了~    

