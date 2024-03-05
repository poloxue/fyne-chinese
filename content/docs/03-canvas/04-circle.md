---
title: 04. 圆 Circle
weight: 4
---

## 圆 Circle

`canvas.Circle` 定义了一个由指定颜色填充的圆形。您还可以设置 `StrokeWidth`，因此显示不同的 `StrokeColor`，如此示例中所示。

圆形将填充通过调用 `Resize()` 或由其控制的布局指定的空间。由于示例将圆形设置为窗口内容，它将调整大小以填充窗口，存在基本的内边距（由主题控制）。

```go
package main

import (
	"image/color"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
)

func main() {
	myApp := app.New()
	w := myApp.NewWindow("圆形")

	circle := canvas.NewCircle(color.White)
	circle.StrokeColor = color.Gray{Y: 0x99}
	circle.StrokeWidth = 5
	w.SetContent(circle)

	w.Resize(fyne.NewSize(100, 100))
	w.ShowAndRun()
}
```

所有这些都是基本类型，可以由我们的驱动程序渲染，无需额外信息。接下来，我们将看看更复杂的类型，从 [`Image`](/docs/03-canvas/05-image) 开始。
