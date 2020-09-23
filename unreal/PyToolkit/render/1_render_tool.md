# Sequencer 批量渲染工具

> &emsp;&emsp;选择 Sequencer 进行批量渲染    
> &emsp;&emsp;通过读取引擎的 ini 配置文件获取用户上次设置的渲染参数    
> &emsp;&emsp;沿用同样的参数进行批量拍屏    

> &emsp;&emsp;这个工具不需要用到 C++ 蓝图    

![界面](//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/render/01/01.png)

## 开启插件

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/render/01/02.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

## 拍屏演示

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/render/01/03.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

> &emsp;&emsp;默认读取 Sequencer 里面的配置    
> &emsp;&emsp;自动进行批量拍屏，拍屏完成之后自动打开输出目录。    
> &emsp;&emsp;进行自定义通道渲染的时候，如果什么通道都不选择，意味着会渲染所有的通道。    

## 手动修改拍屏设置

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/render/01/04.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

> &emsp;&emsp;除了输出目录 输出名称 输出格式 这些面板可以调节的参数外。    
> &emsp;&emsp;其他参数均读取 配置路径 的 ini 文件获取。    
> &emsp;&emsp;这部分的配置和 面板上的配置是同步的。    
> &emsp;&emsp;默认打开界面的时候就会自动将 输出目录 和 输出名称 同步。    

---

> &emsp;&emsp;这里自定义参数使用面板的 复选框 勾选是因为在设置面板上添加并不会保存到 ini 文件里面。    
> &emsp;&emsp;只有触发其他选项的勾选才会一并将这部分配置进行报错，这可能会导致不完全同步。    
> &emsp;&emsp;所以我做了 UI 为准。    

> &emsp;&emsp;另外这个工具只是我业余做的，并没有深度测试，可能会有些 BUG ，欢迎交流~    