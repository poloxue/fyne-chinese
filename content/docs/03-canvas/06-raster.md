---
title: "06. 矢量 Raster"
weight: 6
---

# 矢量 Raster

`canvas.Raster` 类似于图像，但在屏幕上为每个像素精确绘制一个点。这意味着，随着用户界面缩放或图像调整大小，将请求更多像素来填充空间。为此，我们使用一个 `Generator` 函数，如此示例所示——它将用于返回每个像素的颜色。

生成器函数可以基于像素（如此示例中我们为每个像素生成一个新的随机颜色）或基于完整图像。生成完整图像（使用 `canvas.NewRaster()`）更高效，但有时直接控制像素更方便。

```go
package main

import (
	"image/color"
	"math/rand"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
)

func main() {
	myApp := app.New()
	w := myApp.NewWindow("Raster")

	raster := canvas.NewRasterWithPixels(
		func(_, _, w, h int) color.Color {
			return color.RGBA{R: uint8(rand.Intn(255)),
				G: uint8(rand.Intn(255)),
				B: uint8(rand.Intn(255)), A: 0xff}
		})
	// raster := canvas.NewRasterFromImage()
	w.SetContent(raster)
	w.Resize(fyne.NewSize(120, 100))
	w.ShowAndRun()
}
```

如果您的像素数据存储在图像中，您可以通过 `NewRasterFromImage()` 函数加载它，该函数将加载图像以在屏幕上精确显示像素。
