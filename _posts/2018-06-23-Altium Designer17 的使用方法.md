---            
title:  Altium-Designer17-的使用方法
date:   2018-06-23 12:00:00
tag:    工具
---
# Altium-Designer17-的使用方法


制作的过程

㈠ 启动 Altium Designer17 ，建立 PCB 工程，打开 `File > New > PCB Project`

㈡ 元器件原理图

⑴ 在工程 `PRJPCB` 文件中右击，选择 `Add New to project` , 然后再选择 `Schematic Library`.

⑵ 在项目名称的底部选择 `SCH Library > Components > Add > 命名`

⑶ 开始画元器件，然后保存。

㈢ 元器件 PCB 封装

⑴ 建文件与前边类似

⑵ 在顶部选择 `Tools > Component Wizard > Next > (DIP) > Next > Next > Next > Next > 输入引脚数，然后下一步 > 然后命名 > Finish` 完成。

⑶ 手动画：`放置焊盘（快捷键PP）> 按 Tab 键设置焊盘 > 用 Ctrl+M 准确测量一下自己画的封装的各种尺寸 > 然后双击该名称进行改名`，完成。

⑷ 注意，元器件与元器件的封装，引脚标号必须一一对应。

㈣ 原理图

在工程 `PRJPCB` 文件中右击，选择 `Add New to project` , 然后再选择 `Schematic` .

⑴ 在 `Libraries` 中，找到相应的库，输入名称，选择元器件，然后 `Place` 。画原理图。

⑵ 排列标号：`Tools > Annotate > Annotate Schematics > Reset > All > Accept Changes (Create ECO) > Validate Changes > Execute Changes`

⑶ 保存，右击原理图文件，选择 `Compile Document` , 如果没有错误，则完成。

㈤ PCB

在工程 `PRJPCB` 文件中右击，选择 `Add New to project` , 然后再选择 `PCB` .

⑴ 在 `Design > Import > Changes > From` ,把文件拖进来。

⑵ 在 `Design > Rules > Routing > Width > Width` 中修改线条宽度，我这里设置的是 40 mm 。

画完后，在 `PCB` 页面用 `Keep-Out Layer` 画出所需板子的大小形状，注意必须是封闭的形状。选中画出的这些封闭的框框。（一次不能全部选中的话可以按住 `Shift` 依次选中线条）`Design >  Board Shape > Define from selected objects` ，就完成了截板子。

### 友链

<a href="https://blog.csdn.net/kobesdu/article/details/17961143">Altium_Designer如何快速寻找元件和封装</a>

<a href="https://blog.csdn.net/android_lover2014/article/details/55006789">Altium Designer画元器件封装三种方法</a>

> {{ site.prompt }}

<div  align="center">
<img src="https://rengui520.github.io/images/wechart.jpg" width = "200" height = "200"/>