---
title: "01. 盒子 Box"
weight: 1
---

# 盒子 Box

如在[容器和布局](/docs/02-explore/02-container)中讨论的，容器中的元素可以使用布局来排列。本节探讨内置布局及其使用方法。

最常用的布局是 `layout.BoxLayout`，它有两个变体，水平和垂直。盒子布局将所有元素排列在单个行或列中，并可选择间隔以协助对齐。

水平盒子布局，通过 `layout.NewHBoxLayout()` 创建，将项目排列在单行中。盒子中的每个项目的宽度将设置为其 `MinSize().Width`，高度对所有项目而言都是相等的，值为所有 `MinSize().Height` 值中的最大值。该布局可用于容器中，或者你可以使用盒子控件 `widget.NewHBox()`。

垂直盒子布局与之相似，但它将项目排列在一列中。每个项目的高度将设置为最小值，所有宽度将相等，设置为最小宽度中的最大值。

为了在元素之间创建扩展空间（例如，使某些元素左对齐，其他元素右对齐），在项目中添加一个 `layout.NewSpacer()`。间隔符将扩展以填充所有可用空间。在垂直盒子布局开始处添加一个间隔符将导致所有项目底部对齐。你可以在水平排列的开始和结束处各添加一个间隔符，以创建居中对齐。

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
	myWindow := myApp.NewWindow("盒子布局")

	text1 := canvas.NewText("你好", color.White)
	text2 := canvas.NewText("在那里", color.White)
	text3 := canvas.NewText("(右侧)", color.White)
	content := container.New(layout.NewHBoxLayout(), text1, text2, layout.NewSpacer(), text3)

	text4 := canvas.NewText("居中", color.White)
	centered := container.New(layout.NewHBoxLayout(), layout.NewSpacer(), text4, layout.NewSpacer())
	myWindow.SetContent(container.New(layout.NewVBoxLayout(), content, centered))
	myWindow.ShowAndRun()
}
```

