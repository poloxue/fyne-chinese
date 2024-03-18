---
title: "04. 边框布局 Border"
weight: 4
---

# 边框布局 Border

边框布局可能是构建用户界面时使用最广泛的布局之一，因为它允许围绕一个将扩展以填充空间的中心元素定位项目。要创建一个边框容器，你需要将应该在边框位置定位的 `fyne.CanvasObject` 作为构造函数的前四个参数传递。这个语法基本上就是 `container.NewBorder(top, bottom, left, right, center)`，如示例所示。

传递给容器的前四个项目之后的任何项目都将被定位到中心区域，并将扩展以填充可用空间。你也可以将 `nil` 传递给你希望留空的边框参数。

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
	myWindow := myApp.NewWindow("边框布局")

	top := canvas.NewText("顶部栏", color.White)
	left := canvas.NewText("左侧", color.White)
	middle := canvas.NewText("内容", color.White)
	content := container.NewBorder(top, nil, left, nil, middle)
	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
```

请注意，中心的所有项目都将扩展以填充空间（就像它们在 [`layout.MaxLayout`](/docs/04-container/07-max) 容器中一样）。要自己管理该区域，你可以使用任何 `fyne.Container` 作为内容。
