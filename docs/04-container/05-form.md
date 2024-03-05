---
title: "05. 表单布局 Form"
weight: 5
---

# 表单布局 Form

`layout.FormLayout` 类似于两列的 [网格布局](/docs/04-container/02-grid)，但针对应用中的表单布局进行了调整。每个项目的高度将是每行中两个最小高度中的较大者。第一列中所有项目的最大最小宽度将是左侧项目的宽度，而每行中的第二个项目将扩展以填满空间。

这种布局更典型地用于 `widget.Form`（用于验证、提交和取消按钮等），但也可以直接使用 `layout.NewFormLayout()` 作为 `container.New(...)` 的第一个参数。

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/layout"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("表单布局")

	label1 := widget.NewLabel("标签 1")
	value1 := widget.NewLabel("值")
	label2 := widget.NewLabel("标签 2")
	value2 := widget.NewLabel("某些内容")
	grid := container.New(layout.NewFormLayout(), label1, value1, label2, value2)
	myWindow.SetContent(grid)
	myWindow.ShowAndRun()
}
```
