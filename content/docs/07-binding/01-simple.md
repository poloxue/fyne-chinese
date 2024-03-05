---
title: "01. 简单绑定"
weight: 1
---

# 简单绑定

绑定控件的最简单形式是将绑定项作为值传递给它，而不是静态值。许多控件提供了一个`WithData`构造函数，它将接受一个类型化的数据绑定项。要设置绑定，你需要做的就是传递正确的类型。

尽管在初始代码中这看起来可能没有多大好处，但你可以看到它如何确保显示的内容始终与数据源保持最新。你会注意到，我们不需要在`Label`控件上调用`Refresh()`，甚至不需要保留它的引用，但它仍然会适当更新。

```go
package main

import (
	"time"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/data/binding"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	w := myApp.NewWindow("Simple")

	str := binding.NewString()
	str.Set("Initial value")

	text := widget.NewLabelWithData(str)
	w.SetContent(text)

	go func() {
		time.Sleep(time.Second * 2)
		str.Set("A new string")
	}()

	w.ShowAndRun()
}
```

在下一步中，我们将看看如何通过[双向](/docs/07-binding/02-twoway)绑定设置编辑值的控件。
