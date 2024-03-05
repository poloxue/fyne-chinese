---
title: "04. 列表类型"
weight: 4
---

# 列表类型

为了展示如何连接更复杂的类型，我们将看看`List`控件以及数据绑定如何使其更易用。首先，我们创建一个`StringList`数据绑定，这是一个`String`数据类型的列表。一旦我们有了列表类型的数据，我们就可以将这个数据连接到标准的`List`控件。为此，我们使用`widget.NewListWithData`构造函数，这和其他控件类似。

将这段代码与[列表教程](/docs/06-collection/01-list)进行比较，你会看到两个主要变化，第一个是我们将数据类型作为第一个参数传递，而不是长度回调函数。第二个变化是最后一个参数，我们的`UpdateItem`回调。修订版采用`binding.DataItem`值而不是`widget.ListIndexID`。使用这种回调结构时，我们应该`Bind`到模板标签控件而不是调用`SetText`。这意味着如果数据源中的任何字符串发生变化，表格的每个受影响行都将刷新。

```go
package main

import (
	"fmt"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/data/binding"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("List Data")

	data := binding.BindStringList(
		&[]string{"Item 1", "Item 2", "Item 3"},
	)

	list := widget.NewListWithData(data,
		func() fyne.CanvasObject {
			return widget.NewLabel("template")
		},
		func(i binding.DataItem, o fyne.CanvasObject) {
			o.(*widget.Label).Bind(i.(binding.String))
		})

	add := widget.NewButton("Append", func() {
		val := fmt.Sprintf("Item %d", data.Length()+1)
		data.Append(val)
	})
	myWindow.SetContent(container.NewBorder(nil, add, nil, nil, list))
	myWindow.ShowAndRun()
}
```

在我们的演示代码中，有一个“Append”按钮，当点击时，它会向数据源追加一个新值。这样做将自动触发数据变化处理程序并扩展`List`控件以显示新数据。
