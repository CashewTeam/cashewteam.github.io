---
title: Blender AE 导出联动插件
date: 2024-09-30 16:00:00 +800
categories: [Blender, Blender插件]
tags: [Blender, AE, 脚本, 插件]     # TAG names should always be lowercase
description: "Export: Adobe After Effects (.jsx)"
pin: false
---
## Export: Adobe After Effects (.jsx)
Blender AE 导出联动插件<br />
![AE导出](/assets/image/posts/blender/Export-Adobe-After-Effects.jpg)
_io export after effects_

## 使用说明
### 使用自带拓展面板安装（4.2+）
![Extensions](/assets/image/posts/blender/Export-Adobe-After-Effects-1.jpg)
_Get Extensions_
在`编辑`-`偏好设置`-`Get Extensions`面板中搜索`after`<br />
即可找到`Export: Adobe After Effects (.jsx)`直接安装即可。<br />

### 手动安装
![插件面板](/assets/image/posts/blender/Export-Adobe-After-Effects-2.jpg)
_4.2插件面板_
下载得到`io_aftereffects_export_with_curves.py`<br />
在`编辑`-`偏好设置`-`插件`面板，选择并安装`.py`文件即可<br />
4.2 版本点击右上角按钮选择`Install from Disk...`

### 导出 jsx 脚本
![Blender导出](/assets/image/posts/blender/Export-Adobe-After-Effects-3.jpg)
_4.2 插件面板_
选择好场景中的物体后，在`文件`-`导出`-`Adobe After Effects (.jsx)`导出当前场景为jsx脚本。

### AE 中运行脚本
![运行脚本](/assets/image/posts/blender/Export-Adobe-After-Effects-4.jpg)
_AE 中运行脚本_
在 AE 中点击`文件`-`脚本`-`运行脚本文件`<br />
选择刚才导出的 jsx 文件，在弹出面板设置合成名，<br />
打开刚才脚本生成的合成即可看到 Blender 中的物体已经导入进来了。<br />
如果没有成功可能是没有在`AE首选项`-`脚本和表达式`-打开`允许脚本写入文件和访问网络`
![导入成功](/assets/image/posts/blender/Export-Adobe-After-Effects-5.jpg)
_导入成功_

Blender 中除了摄像机和灯光外都会转换成空物体导入进来，如果需要样条路径或是模型某个位置，可以在Blender中绑定空物体到需要的位置。<br />
插件源码注释中讲解了 Blender 到 AE 摄像机等数据转换的具体过程，感兴趣的可以自行学习。

## 下载
[Blender拓展](https://extensions.blender.org/add-ons/io-export-after-effects/)<br />
[Github](https://github.com/vitos1k/pipelinetools)<br />
[度盘链接](https://pan.baidu.com/s/1W_It9K_Z16_NtvddyW4mEQ?pwd=gspp)<br />
