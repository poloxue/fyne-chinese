---
title: "02. 双向绑定" 
weight: 2
---

# 双向绑定

到目前为止，我们已经看到了数据绑定作为一种方式来保持用户界面元素更新。然而，更常见的需求是从UI控件更新值并保持数据在各处都是最新的。值得庆幸的是，Fyne提供的绑定是“双向”的，这意味着值既可以被推入其中也可以被读出。数据的更改将被通知到所有连接的代码，无需任何额外的代码。

为了看到这个功能的实际操作，我们可以更新最后的测试应用，以显示一个`Label`和一个`Entry`，它们绑定到同一个值。通过这样设置，你可以看到通过entry编辑值也会更新label中的文本。这一切都可以在不调用refresh或在代码中引用控件的情况下实现。

通过将你的应用移动到使用数据绑定，你可以停止保存指向所有控件的指针。相反，通过捕获数据作为一组绑定的值，你的用户界面可以是完全独立的代码。更清晰易读，更易于管理。

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/data/binding"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	w := myApp.NewWindow("Two Way")

	str := binding.NewString()
	str.Set("Hi!")

	w.SetContent(container.NewVBox(
		widget.NewLabelWithData(str),
		widget.NewEntryWithData(str),
	))

	w.ShowAndRun()
}
```

接下来，我们将看看如何在我们的数据中添加[转换](/docs/07-binding/03-conversion)。
