---
title: "02. 文本 Text"
weight: 2
---

## 文本 Text

`canvas.Text` 用于 Fyne 内的所有文本渲染。它通过指定文本和文本颜色来创建。文本使用当前主题指定的默认字体渲染。

文本对象允许某些配置，如 `Alignment` 和 `TextStyle` 字段，如此示例中所示。如果你想使用等宽字体，可以指定 `fyne.TextStyle{Monospace: true}`。

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
	w := myApp.NewWindow("文本")

	text := canvas.NewText("文本对象", color.White)
	text.Alignment = fyne.TextAlignTrailing
	text.TextStyle = fyne.TextStyle{Italic: true}
	w.SetContent(text)

	w.ShowAndRun()
}
```

通过指定 `FYNE_FONT` 环境变量，可以使用另一种字体。使用这个来设置一个 `.ttf` 文件，代替 Fyne 工具包或当前主题提供的字体。

