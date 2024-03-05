---
title: "07. 工具栏 Toolbar"
weight: 7
---

# 工具栏 Toolbar

工具栏控件使用图标创建一行动作按钮来表示每个操作。`widget.NewToolbar(...)` 构造函数接受一系列 `widget.ToolbarItem` 参数。内置的工具栏项目类型有动作，分隔符和空格器。

最常用的项目是动作，使用 `widget.NewToolbarAction(..)` 函数创建。动作有两个参数，第一个是要绘制的图标资源，后一个是点击时调用的 `func()`。这样创建了一个标准的工具栏按钮。

你可以使用 `widget.NewToolbarSeparator()` 在工具栏中的项目之间创建一个小分隔符（通常是一个细的垂直线）。最后，你可以使用 `widget.NewToolbarSpacer()` 在元素之间创建一个灵活的空间。这最适合用于右对齐列表中的工具栏项目。

工具栏应始终位于内容区域的顶部，所以通常使用 `layout.BorderLayout` 将其添加到 `fyne.Container` 中，以便将其与其他内容对齐。

```go
package main

import (
	"log"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/theme"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("工具栏控件")

	toolbar := widget.NewToolbar(
		widget.NewToolbarAction(theme.DocumentCreateIcon(), func() {
			log.Println("新建文档")
		}),
		widget.NewToolbarSeparator(),
		widget.NewToolbarAction(theme.ContentCutIcon(), func() {}),
		widget.NewToolbarAction(theme.ContentCopyIcon(), func() {}),
		widget.NewToolbarAction(theme.ContentPasteIcon(), func() {}),
		widget.NewToolbarSpacer(),
		widget.NewToolbarAction(theme.HelpIcon(), func() {
			log.Println("显示帮助")
		}),
	)

	content := container.NewBorder(toolbar, nil, nil, nil, widget.NewLabel("内容"))
	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
```

