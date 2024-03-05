---
title: "06. 居中布局 Center"
weight: 6
---

# 居中布局

`layout.CenterLayout` 将其容器中的所有项目都组织在可用空间的中心。这些对象将按照它们被传递到容器的顺序绘制，最后传递的对象将被绘制在最顶部。

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
	myWindow := myApp.NewWindow("Center Layout")

	img := canvas.NewImageFromResource(theme.FyneLogo())
	img.FillMode = canvas.ImageFillOriginal
	text := canvas.NewText("Overlay", color.Black)
	content := container.New(layout.NewCenterLayout(), img, text)

	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
```

中心布局使所有项目保持其最小大小，如果你希望扩展项目以填充空间，那么请参见[`layout.MaxLayout`](/docs/04-container/07-max)。

