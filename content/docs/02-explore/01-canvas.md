---
title: "01. Canvas 和 CanvasObject"
weight: 1
---

## Canvas 和 CanvasObject

在Fyne中，画布（Canvas）是应用程序绘制的区域。每个窗口都有一个画布，你可以通过`Window.Canvas()`访问它，但通常你会发现`Window`上的函数可以避免直接访问画布。

Fyne中可以绘制的所有内容都是`CanvasObject`类型。这个示例打开了一个新窗口，然后通过设置窗口画布的内容来展示不同类型的基本图形元素。如文本和圆形示例所示，每种类型的对象都有许多定制方式。

除了使用`Canvas.SetContent()`更改显示的内容外，还可以更改当前可见的内容。例如，如果你更改了矩形的`FillColour`，可以使用`rect.Refresh()`请求刷新这个已存在的组件。

```go
package main

import (
	"image/color"
	"time"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Canvas")
	myCanvas := myWindow.Canvas()

	blue := color.NRGBA{R: 0, G: 0, B: 180, A: 255}
	rect := canvas.NewRectangle(blue)
	myCanvas.SetContent(rect)

	go func() {
		time.Sleep(time.Second)
		green := color.NRGBA{R: 0, G: 180, B: 0, A: 255}
		rect.FillColor = green
		rect.Refresh()
	}()

	myWindow.Resize(fyne.NewSize(100, 100))
	myWindow.ShowAndRun()
}
```

我们可以用相同的方式绘制许多不同的绘图元素，如圆形和文本。

```go
func setContentToText(c fyne.Canvas) {
	green := color.NRGBA{R: 0, G: 180, B: 0, A: 255}
	text := canvas.NewText("Text", green)
	text.TextStyle.Bold = true
	c.SetContent(text)
}

func setContentToCircle(c fyne.Canvas) {
	red := color.NRGBA{R: 0xff, G: 0x33, B: 0x33, A: 0xff}
	circle := canvas.NewCircle(color.White)
	circle.StrokeWidth = 4
	circle.StrokeColor = red
	c.SetContent(circle)
}
```

### 控件 Widget

`fyne.Widget`是一种特殊类型的画布对象，它与交互元素关联。在控件中，逻辑与其外观（也称为`WidgetRenderer`）是分开的。

控件也是`CanvasObject`类型，因此我们可以将窗口的内容设置为单个控件。看看我们如何创建一个新的`widget.Entry`并将其设置为窗口的内容。

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Widget")

	myWindow.SetContent(widget.NewEntry())
	myWindow.ShowAndRun()
}
```

这段描述说明了如何在Fyne应用程序中处理和更新画布内容，以及如何使用控件来创建交互式用户界面元素。
