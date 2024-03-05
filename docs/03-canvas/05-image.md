---
title: "05. 图片 Image"
weight: 5
---

## 图片 Image

`canvas.Image` 在 Fyne 中代表一个可缩放的图像资源。它可以从资源（如示例所示）、图像文件、包含图像的 URI 位置、`io.Reader` 或内存中的 Go `image.Image` 加载。

默认的图像填充模式是 `canvas.ImageFillStretch`，它会导致图像填充指定的空间（通过 `Resize()` 或布局）。或者，你可以使用 `canvas.ImageFillContain` 以确保保持纵横比并且图像在边界内。此外，你可以使用 `canvas.ImageFillOriginal`（如此示例中所用），以确保它也具有等于原始图像大小的最小尺寸。

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
	"fyne.io/fyne/v2/theme"
)

func main() {
	myApp := app.New()
	w := myApp.NewWindow("图像")

	image := canvas.NewImageFromResource(theme.FyneLogo())
	// image := canvas.NewImageFromURI(uri)
	// image := canvas.NewImageFromImage(src)
	// image := canvas.NewImageFromReader(reader, name)
	// image := canvas.NewImageFromFile(fileName)
	image.FillMode = canvas.ImageFillOriginal
	w.SetContent(image)

	w.ShowAndRun()
}
```

图像可以是基于位图的（如 PNG 和 JPEG）或基于矢量的（如 SVG）。我们建议尽可能使用可缩放图像，因为它们在大小变化时继续渲染良好。在使用原始图像大小时要小心，因为它们可能不会完全按预期与不同的用户界面比例一致。由于 Fyne 允许整个用户界面缩放，一个 25px 的图像文件可能与一个 25 高度的 fyne 对象不同。
