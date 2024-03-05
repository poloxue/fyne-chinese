---
title: "04. 复选框 Choices"
weight: 4
---

# 复选框 Choices

有各种控件可用于向用户展示选择，包括复选框、单选按钮组和下拉选择框。

`widget.Check` 提供一个简单的是/否选择，使用字符串标签创建。这些控件每一个都接受一个 "changed" `func(...)`，其中参数类型适用于它们。因此，`widget.NewCheck(..)` 接受一个 `string` 参数作为标签和一个 `func(bool)` 参数作为更改处理器。你也可以使用 `Checked` 字段来获取布尔值。

单选按钮控件类似，但第一个参数是表示每个选项的 `string` 切片。这次更改函数期望一个 `string` 参数，以返回当前选定的值。调用 `widget.NewRadioGroup(...)` 来构造单选按钮组控件，你可以稍后使用这个引用来读取 `Selected` 字段，而不是使用更改回调。

下拉选择控件在构造函数签名上与单选按钮控件相同。调用 `widget.NewSelect(...)` 将显示一个按钮，当点击时会显示一个弹出窗口，用户可以从中进行选择。对于长列表的选项，这更加合适。

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
	myWindow := myApp.NewWindow("选择控件")

	check := widget.NewCheck("可选", func(value bool) {
		log.Println("复选框设置为", value)
	})
	radio := widget.NewRadioGroup([]string{"选项 1", "选项 2"}, func(value string) {
		log.Println("单选按钮设置为", value)
	})
	combo := widget.NewSelect([]string{"选项 1", "选项 2"}, func(value string) {
		log.Println("选择设置为", value)
	})

	myWindow.SetContent(container.NewVBox(check, radio, combo))
	myWindow.ShowAndRun()
}
```
