---
title: "03. 内置控件 Widget"
weight: 3
---

# 标准 Widget (在 `widget` 包中）

### 手风琴（Accordion）

手风琴显示一个手风琴项目列表。每个项目由一个按钮表示，当点击时会展示一个详细视图。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/accordion-light.png)

### 按钮（Button）

[按钮](/docs/05-widget/02-button)控件有一个文本标签和图标，两者都是可选的。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/button-light.png)


### 卡片（Card）

卡片控件以头部和副标题将元素分组，所有这些都是可选的。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/card-light.png)

### 复选框（Check）

复选框控件有一个文本标签和一个选中（或未选中）的图标。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/check-light.png)

### 输入框（Entry）

[输入框](/docs/05-widget/03-entry)控件允许在聚焦时输入简单文本。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/entry-light.png)

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/entry-valid-light.png)

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/entry-invalid-light.png)

密码输入框控件隐藏文本输入，并添加一个按钮以显示文本。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/password-light.png)

### 文件图标（FileIcon）

文件图标为各种类型的文件提供有用的标准图标。它显示文件类型的指示图标并显示文件类型的扩展名。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/fileicon-light.png)

### 表单（Form）

[表单](/docs/05-widget/05-form)控件是一个两列网格，每行有一个标签和一个控件（通常是输入）。如果应该显示任何表单控制按钮，则网格的最后一行将包含它们。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/form-light.png)

### 超链接（Hyperlink）

超链接控件是一个具有适当填充和布局的文本组件。点击时，URL会在默认网络浏览器中打开。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/hyperlink-light.png)

### 图标（Icon）

图标控件是一个基本的图像组件，加载资源以匹配主题。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/icon-light.png)

### 标签（Label）

[标签](/docs/05-widget/01-label)控件是一个具有适当填充和布局的标签组件。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/label-light.png)

### 进度条（Progress bar）

[进度条](/docs/05-widget/06-progressbar)控件创建一个表示进度的水平面板。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/progress-light.png)

无限进度条控件创建一个表示无限等待的水平面板。一个无限进度条会重复从0%循环到100%，直到调用Stop()。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/progressinf-light.png)

### 单选组（RadioGroup）

单选组控件有一个文本标签列表和每个旁边的单选检查图标。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/radiogroup-light.png)

### 选择（Select）

选择控件有一个选项列表，显示当前选项，并在点击时触发一个事件函数。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/select-light.png)

### 选择输入（SelectEntry）

选择输入控件在选择控件中添加了一个可编辑组件。用户可以选择一个选项或输入自己的值。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/selectentry-light.png)

### 分隔符（Separator）

分隔符控件在其他元素之间显示一条分隔线。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/separator-light.png)

### 滑块（Slider）

滑块是一个可以在两个固定值之间滑动的控件。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/slider-light.png)

### 文本网格（TextGrid）

文本网格是一个等宽的字符网格。这是设计用来被文本编辑器、代码预览或终端仿真器使用的。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/textgrid-light.png)

### 工具栏（Toolbar）

[工具栏](/docs/05-widget/07-toolbar)控件创建一个水平的工具按钮列表。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/toolbar-light.png)

## 集合控件（在`widget`包中）

集合控件提供高级缓存功能，以提供大量数据的高性能渲染。这确实导致了更复杂的构造器，但对于它启用的结果来说是一个好平衡。这些控件中的每一个都使用了一系列回调，最小集由它们的构造函数定义，其中包括数据大小，可以重用的模板项目的创建，以及将数据应用到即将添加到显示中的控件的函数。

### 列表（List）

[列表](/docs/06-collection/01-list)提供了许多子项的高性能垂直滚动。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/list-light.png)

### 表格（Table）

[表格](/docs/06-collection/02-table)提供了许多子项的高性能滚动二维显示。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/table-light.png)

## 树形（Tree）

[树形](/docs/06-collection/03-tree) 控件提供了一个高性能的垂直滚动列表，可以展开以显示子元素。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/table-light.png)

## 容器控件（在container包中）

容器控件类似于常规容器，但它们提供了一些额外的功能。

### 应用标签页

应用标签页控件允许从一系列标签项中切换可见内容。每个项都由顶部的一个按钮代表。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/apptabs-light.png)

### 滚动
滚动容器定义了一个比内容小的容器。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/slider-light.png)

### 分割

分割容器定义了一个容器，其大小在两个子项之间分割。

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/widgets/split-light.png)

