---
title: "02. 容器与布局" 
weight: 2
---

## 容器与布局

在前一个示例中，我们看到了如何将`CanvasObject`设置为`Canvas`的内容，但只显示一个视觉元素并不是很有用。要显示多个项，我们使用`Container`类型。

由于`fyne.Container`也是一个`fyne.CanvasObject`，我们可以将它设置为`fyne.Canvas`的内容。在这个示例中，我们创建了3个文本对象，然后使用`container.NewWithoutLayout()`函数将它们放入一个容器中。由于没有设置布局，我们可以像你看到的那样用`text2.Move()`移动元素。

```go
package main

import (
	"image/color"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
	"fyne.io/fyne/v2/container"
	//"fyne.io/fyne/v2/layout"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Container")
	green := color.NRGBA{R: 0, G: 180, B: 0, A: 255}

	text1 := canvas.NewText("Hello", green)
	text2 := canvas.NewText("There", green)
	text2.Move(fyne.NewPos(20, 20))
	content := container.NewWithoutLayout(text1, text2)
	// content := container.New(layout.NewGridLayout(2), text1, text2)

	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
```

`fyne.Layout`实现了一种在容器内组织项目的方法。通过在这个示例中取消注释`container.New()`行，你改变了容器以使用2列的网格布局。运行此代码并尝试调整窗口大小，看看布局如何自动配置窗口的内容。还要注意，`text2`的手动位置被布局代码忽略了。

要了解更多，你可以查看[`布局组件`](/docs/02-explore/04-layouts)。
