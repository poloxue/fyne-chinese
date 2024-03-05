---
title: "03. 网格包装 Grid Wrap"
weight: 3
---

# 网格包装 Grid Wrap

与之前的网格布局一样，网格包装布局在网格模式中创建元素的排列。然而，这种网格没有固定数量的列，而是为每个单元格使用固定大小，然后将内容流动到需要显示项目的尽可能多的行中。

使用 `layout.NewGridWrapLayout(size)` 创建网格包装布局，其中 size 指定要应用于所有子元素的大小。然后将此布局作为第一个参数传递给 `container.New(...)`。根据容器的当前大小计算列数和行数。

最初，网格包装布局将有一个单列，如果您调整它的大小（如代码注释中所示），它将重新排列子元素以填充空间。

```go
package main

import (
	"image/color"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/layout"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("网格包装布局")

	text1 := canvas.NewText("1", color.White)
	text2 := canvas.NewText("2", color.White)
	text3 := canvas.NewText("3", color.White)
	grid := container.New(layout.NewGridWrapLayout(fyne.NewSize(50, 50)),
		text1, text2, text3)
	myWindow.SetContent(grid)

	// myWindow.Resize(fyne.NewSize(180, 75))
	myWindow.ShowAndRun()
}
```
