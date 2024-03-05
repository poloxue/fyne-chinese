---
title: "04. 布局组件"
weight: 4
---

## 布局组件

### 水平盒（HBox）

水平盒将项目以水平行的方式排列。容器中的每个元素将具有相同的高度（容器中最高项目的高度），并且对象将按其最小宽度左对齐。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/layouts/hbox-light.png)

### 垂直盒（VBox）

垂直盒将项目以垂直列的方式排列。容器中的每个元素将具有相同的宽度（容器中最宽项目的宽度），并且对象将按其最小高度顶部对齐。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/layouts/vbox-light.png)

### 居中（Center）

居中布局将所有容器元素定位在容器的中心。每个对象都将设置为其最小尺寸。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/layouts/center-light.png)

### 表单（Form）

表单布局将项目成对排列，其中第一列为最小宽度。这通常用于表单中的标签元素，其中标签位于第一列，其描述的项目位于第二列。你应该总是向表单布局添加偶数个元素。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/layouts/form-light.png)

### 网格（Grid）

网格布局在可用空间中均匀排列项目。指定列数，对象水平定位，直到达到列数，此时开始新的行。所有对象具有相同的大小，即宽度除以列总数，高度将是总高度除以所需行数减去填充。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/layouts/grid-light.png)

### 网格包裹（GridWrap）

网格包裹布局将所有项目沿一行流动排列，如果空间不足，则换到新行。所有对象将设置为相同的大小，即传递给布局的大小。这种布局可能不会尊重项目的MinSize以管理这种统一布局。通常用于文件管理器或图像缩略图列表。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/layouts/gridwrap-light.png)

### 边框（Border）

边框布局支持在可用空间外围定位项目。边框传递指向对象的指针（顶部、左侧、底部、右侧）。容器中未定位在边框上的所有项目将填充剩余空间。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/layouts/border-light.png)

### 最大（Max）

最大布局将所有容器元素定位以填充可用空间。对象都将是全尺寸的，并按照它们被添加到容器中的顺序绘制（最后添加的在最上面）。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/layouts/max-light.png)

### 填充（Padded）

填充布局将所有容器元素定位以填充可用空间，但在外围有一小块填充。填充的大小是主题特定的。对象都将按照它们被添加到容器中的顺序绘制（最后添加的在最上面）。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/layouts/padded-light.png)

## 组合布局

通过使用多个布局，可以构建更复杂的应用程序结构。每个具有自己布局的多个容器可以嵌套，仅使用上面列出的标准布局创建完整的用户界面布局。例如，一个用于页眉的水平盒，一个用于左侧文件面板的垂直盒，以及内容区域中的网格包装布局 - 所有这些都放在使用边框布局的容器内，可以构建下面所示的结果。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/layouts/combined-light.png)
