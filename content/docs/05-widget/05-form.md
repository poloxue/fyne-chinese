---
title: "05. 表单 Form"
weight: 5
---

# 表单 Form

表单控件用于排列许多输入字段、标签以及可选的取消和提交按钮。在其最简单的形式中，它将标签对齐到每个输入控件的左侧。通过设置OnCancel或OnSubmit，表单将添加一个按钮栏，当适当时调用指定的处理程序。

可以通过传递`widget.FormItem`列表使用`widget.NewForm(...)`创建控件，或者使用示例中所示的`&widget.Form{}`语法。还有一个有用的`Form.Append(label, widget)`，可用于另一种语法。

在这个例子中，我们创建了两个输入框，其中一个是“多行”的（类似HTML TextArea）来保存值。有一个OnSubmit处理程序，在关闭窗口（因此是应用程序）之前打印信息。

```go
package main

import (
	"log"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("表单控件")

	entry := widget.NewEntry()
	textArea := widget.NewMultiLineEntry()

	form := &widget.Form{
		Items: []*widget.FormItem{ // 我们可以在构造函数中指定项
			{Text: "输入框", Widget: entry}},
		OnSubmit: func() { // 可选，处理表单提交
			log.Println("表单提交：", entry.Text)
			log.Println("多行：", textArea.Text)
			myWindow.Close()
		},
	}

	// 我们也可以追加项目
	form.Append("文本", textArea)

	myWindow.SetContent(form)
	myWindow.ShowAndRun()
}
```
