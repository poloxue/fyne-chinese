---
title: "01. 矩形 Rectangle"
weight: 1
---

## 矩形 Rectangle

`canvas.Rectangle` 是 Fyne 中最简单的画布对象。它显示指定颜色的区块。您也可以使用 `FillColor` 字段设置颜色。

在这个示例中，矩形填充了窗口，因为它是唯一的内容元素。

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
	w := myApp.NewWindow("矩形")

	rect := canvas.NewRectangle(color.White)
	w.SetContent(rect)

	w.Resize(fyne.NewSize(150, 100))
	w.ShowAndRun()
}
```

其他的 `fyne.CanvasObject` 类型有更多的配置，让我们[接下来](/docs/03-canvas/02-text)看看 `canvas.Text`。
