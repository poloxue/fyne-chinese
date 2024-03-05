---
title: "03. 线条 Line"
weight: 3
---

## 线条 Line

`canvas.Line` 对象从 `Position1`（默认是左上角）画到 `Position2`（默认是右下角）。你可以指定它的颜色，并且可以改变笔触宽度，否则默认为 `1`。

线的位置可以使用 `Position1` 或 `Position2` 字段，或者使用 `Move()` 和 `Resize()` 函数来操作。例如，宽度为 0 的区域会显示为垂直线，而高度为 0 则会是水平线。

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
	w := myApp.NewWindow("线条")

	line := canvas.NewLine(color.White)
	line.StrokeWidth = 5
	w.SetContent(line)

	w.Resize(fyne.NewSize(100, 100))
	w.ShowAndRun()
}
```

线条通常用于自定义布局或手动控制。与文本不同，它们没有自然（最小）大小，但可以在复杂布局中产生出色的效果。
