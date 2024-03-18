---
title: "02. 按钮 Button"
weight: 2
---

# 按钮 Button

按钮控件可以包含文本、图标或两者，构造函数是 `widget.NewButton()` 和 `widget.NewButtonWithIcon()`。要创建一个文本按钮，只有两个参数，`string` 内容和一个没有参数的 `func()`，当按钮被点击时将调用此函数。参见示例以了解如何创建它。

带有图标的按钮构造函数包含一个额外的参数，即包含图标数据的 `fyne.Resource`。`theme` 包中的内置图标都适当地适应主题更改。如果将自己的图像加载为资源，你可以传入自己的图像 - 诸如 `fyne.LoadResourceFromPath()` 的助手可能会有所帮助，尽可能推荐捆绑资源。

要创建仅带图标的按钮，你应该将 "" 作为标签参数传递给 `widget.NewButtonWithIcon()`。

```go
package main

import (
	"log"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
	//"fyne.io/fyne/v2/theme"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("按钮控件")

	content := widget.NewButton("点击我", func() {
		log.Println("点击")
	})

	//content := widget.NewButtonWithIcon("首页", theme.HomeIcon(), func() {
	//	log.Println("点击首页")
	//})

	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
```
