---
title: "07. 最大布局 Max"
weight: 7
---

# 最大布局 Max

`layout.MaxLayout`是最简单的布局，它将容器中的所有项目设置为与容器相同的大小。这通常在一般的容器中不太有用，但在组合控件时可能适用。

最大布局会扩展容器，使其至少与最大项目的最小大小相同。对象将按照它们传递给容器的顺序被绘制，最后传递的对象将被绘制在最上面。

```go
package main

import (
	"image/color"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/layout"
	"fyne.io/fyne/v2/theme"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Max Layout")

	img := canvas.NewImageFromResource(theme.FyneLogo())
	text := canvas.NewText("Overlay", color.Black)
	content := container.New(layout.NewMaxLayout(), img, text)

	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
```

