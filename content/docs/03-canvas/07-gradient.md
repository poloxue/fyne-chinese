---
title: "07. 渐变 Gradient"
weight: 7
---

# 渐变 Gradient

最后一个画布原始类型是 Gradient，可用作 `canvas.LinearGradient` 和 `canvas.RadialGradient`，用于绘制从一种颜色到另一种颜色的渐变，有多种模式。你可以使用 `NewHorizontalGradient()`、`NewVerticalGradient()` 或 `NewRadialGradient()` 创建渐变。

要创建一个渐变，你需要一个起始颜色和结束颜色——画布会计算其中的每一个颜色。在这个示例中，我们使用 `color.Transparent` 来展示如何使用渐变（或任何其他类型）通过透明度值在背后的内容上实现半透明效果。

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
	w := myApp.NewWindow("渐变")

	gradient := canvas.NewHorizontalGradient(color.White, color.Transparent)
	//gradient := canvas.NewRadialGradient(color.White, color.Transparent)
	w.SetContent(gradient)

	w.Resize(fyne.NewSize(100, 100))
	w.ShowAndRun()
}
```
