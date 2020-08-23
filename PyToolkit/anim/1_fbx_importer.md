
# 动画导入比较面板

> &emsp;&emsp;本工具完全使用原生 Unreal Python 实现，没有利用 C++ API 的蓝图
> &emsp;&emsp;这个工具用来比以前的 FBX 动画和更新的 FBX 动画帧数是否一致。
> &emsp;&emsp;其实这个功能很鸡肋，但是借助 FBX SDK 其实可以读取很多 FBX 的内部信息进行检查的。
> &emsp;&emsp;关于这部分，我没有在这里展开，只是演示了可行性~

![界面](//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/anim/01/00.png)

## 开启插件

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/anim/01/01.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

## 获取动画资源

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/anim/01/02.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

> &emsp;&emsp;选中动画资源添加到文件路径中，会自自动查找当前目录下的动画资源。

## 将新的动画资源添加到右侧的比较列表

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/anim/01/03.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>


> &emsp;&emsp;添加动画可以使用上方的两个按钮手动选择文件进行添加
> &emsp;&emsp;也可以直接将文件拖拽到面板上

## 状态说明

![说明](//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/anim/01/04.png)

> &emsp;&emsp;比较面板有三种状态
> &emsp;&emsp;绿色勾选表示关键帧数量一致
> &emsp;&emsp;红色打叉表示不一致
> &emsp;&emsp;感叹号表示没有找到匹配项

---

> &emsp;&emsp;这里的匹配要求 FBX 为 bake 全帧，且没有无用关键帧。（并没有用 FBX-SDK 读取文件里面所有的关键帧，只是读取了外部设定里的帧数） 

## 右键菜单

<video src="//cdn.jsdelivr.net/gh/FXTD-ODYSSEY/CG_wiki@gh-pages/PyToolkit/_img/anim/01/05.mp4" autoplay="autoplay" loop="loop" style="width: 100%; height:100%;"></video>

> &emsp;&emsp;第一个选项可以打开导入 FBX 文件的目录
> &emsp;&emsp;第二个选项可以删除当前选中的
> &emsp;&emsp;第三个选项可以将当前选中的进行导入操作

