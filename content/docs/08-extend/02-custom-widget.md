---
title: "02. 自定义控件 Widget"
weight: 2
---

## 自定义控件 Widget"

标准控件与 Fyne 一起提供，旨在支持标准用户交互和需求。由于 GUI 经常需要提供自定义功能，因此可能需要编写自定义控件。本文概述了如何进行。

一个控件被分为两个区域 - 每个都实现一个标准接口 - `fyne.Widget` 和 `fyne.WidgetRenderer`。控件定义行为和状态，而渲染器用于定义它应如何绘制到屏幕上。

### fyne.Widget

Fyne 中的控件简单来说是一个有状态的画布对象，其渲染定义与主逻辑分离。从 `fyne.Widget` 接口可以看出，必须实现的内容并不多。

```go
type Widget interface {
	CanvasObject

	CreateRenderer() WidgetRenderer
}
```

由于控件需要像任何其他画布项目一样被使用，我们从相同的接口继承。为了省去编写所有必需的函数，我们可以使用 `widget.BaseWidget` 类型，它处理了基础内容。

每个控件定义将包含比接口要求更多的内容。在 Fyne 控件中导出定义行为的字段是标准做法（就像 `canvas` 包中定义的原语一样）。

例如，看看 `widget.Button` 类型：

```go
type Button struct {
	BaseWidget
	Text  string
	Style ButtonStyle
	Icon  fyne.Resource

	OnTapped func()
}
```

你可以看到这些项目如何存储有关控件行为的状态，但没有关于它如何呈现的信息。

### fyne.WidgetRenderer

控件渲染器负责管理一组 `fyne.CanvasObject` 原语，这些原语组合在一起创建了我们控件的设计。它很像 `fyne.Container`，但有自定义布局和一些额外的主题处理。

每个控件都必须提供一个渲染器，但完全可以重用另一个控件的渲染器 - 特别是如果你的控件是另一个标准控件的轻量级包装。

```go
type WidgetRenderer interface {
	Layout(Size)
	MinSize() Size

	Refresh()
	Objects() []CanvasObject
	Destroy()
}
```

可以看到 `Layout(Size)` 和 `MinSize()` 函数类似于 `fyne.Layout` 接口，但没有 `[]fyne.CanvasObject` 参数 - 这是因为控件确实需要布局，但它控制哪些对象将被包含。

`Refresh()` 方法在绘制的控件发生变化或主题被更改时触发。在任一情况下，我们可能需要调整它的外观。最后，当这个渲染器不再需要时，会调用 `Destroy()` 方法，因此它应该清除任何可能泄漏的资源。

再次与按钮控件比较 - 它的 `fyne.WidgetRenderer` 实现基于以下类型：

```go
type buttonRenderer struct {
	icon   *canvas.Image
	label  *canvas.Text
	shadow *fyne.CanvasObject

	objects []fyne.CanvasObject
	button  *Button
}
```

可以看到它有字段来缓存实际图像、文本和阴影画布对象用于绘制。它跟踪 `fyne.WidgetRenderer` 所需的对象切片以方便使用。

最后它保留对 `widget.Button` 的引用以获取所有状态信息。在 `Refresh()` 方法中，它将根据 `widget.Button` 类型中的任何更改更新图形状态。

### 整合

基本的控件将扩展 `widget.BaseWidget` 类型并声明控件持有的任何状态。`CreateRenderer()` 函数必须存在并返回一个新的 `fyne.WidgetRenderer` 实例。Fyne 中的控件和驱动代码将确保这被相应地缓存 - 如果
