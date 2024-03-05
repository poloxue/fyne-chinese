---
title: "03. 输入框 Entry"
weight: 3
---

# 输入框 Entry

输入控件（Entry widget）用于用户输入简单文本内容。可以通过`widget.NewEntry()`构造函数简单地创建一个输入控件。创建控件时，保留一个引用，以便以后可以访问其`Text`字段。还可以使用`OnChanged`回调函数，每当内容变化时都会收到通知。

输入控件还可以有验证功能，用于验证输入的文本。这可以通过设置`Validator`字段为`fyne.StringValidator`来完成。你还可以设置`PlaceHolder`文本，并且设置输入控件为`MultiLine`以接受多行文本。

```go
package main

import (
	"log"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Entry Widget")

	input := widget.NewEntry()
	input.SetPlaceHolder("Enter text...")

	content := container.NewVBox(input, widget.NewButton("Save", func() {
		log.Println("Content was:", input.Text)
	}))

	myWindow.SetContent(content)
	myWindow.ShowAndRun()
}
```

你还可以使用`NewPasswordEntry()`函数创建一个密码输入控件（内容被隐藏）。
