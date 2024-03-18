---
title: "01. 标签 Label "
weight: 1
---

# 标签 Label 

Widgets 是 Fyne 应用程序 GUI 的主要组件，它们可以被用在任何一个基本的 `fyne.CanvasObject` 可以使用的地方。它们管理用户交互，并且总是与当前主题相匹配。

Label widget 是最简单的一个 - 它向用户展示文本。与 `canvas.Text` 不同，它可以处理一些简单的格式化（如 `\n`）和换行（通过设置 `Wrapping` 字段）。
你可以通过调用 `widget.NewLabel("some text")` 来创建一个标签，结果可以被赋值给一个变量或直接传递给一个容器。

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Label Widget")

	content := widget.NewLabel("text")

	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
```
