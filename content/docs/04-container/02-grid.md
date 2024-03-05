---
title: "02. 网格 Grid"
weight: 2
---

# 网格 Grid

网格布局将容器的元素以网格模式布置，具有固定数量的列。项目将填充单个行，直到达到列数，之后将创建新行。垂直空间将在对象的每一行之间平均分配。

使用 `layout.NewGridLayout(cols)` 创建网格布局，其中 cols 是您希望每行中有的项目（列）数量。然后将此布局作为第一个参数传递给 `container.New(...)`。

如果您调整容器的大小，则每个单元格将平等地调整大小，以分享可用空间。

```go
package main

import (
	"image/color"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/layout"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("网格布局")

	text1 := canvas.NewText("1", color.White)
	text2 := canvas.NewText("2", color.White)
	text3 := canvas.NewText("3", color.White)
	grid := container.New(layout.NewGridLayout(2), text1, text2, text3)
	myWindow.SetContent(grid)
	myWindow.ShowAndRun()
}
```
