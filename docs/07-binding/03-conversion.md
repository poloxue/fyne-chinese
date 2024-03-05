---
title: "03. 数据转换"
weight: 3
---

# 数据转换

到目前为止，我们使用的数据绑定是数据类型与输出类型匹配的情况（例如`String`与`Label`或`Entry`）。通常，将需要以不同于原始格式的方式展示数据。为此，`binding`包提供了许多有用的转换函数。

最常见的用途是将不同类型的数据转换为字符串，以便在`Label`或`Entry`控件中显示。看看我们如何使用`binding.FloatToString`将`Float`转换为`String`。原始值可以通过移动滑块来编辑。每次数据变化时，它都会运行转换代码并更新任何连接的控件。

也可以使用格式字符串为用户界面添加更自然的输出。你可以看到我们的`short`绑定也是将`Float`转换为`String`，但通过使用`WithFormat`助手，我们可以传递一个格式字符串（类似于`fmt`包）来提供自定义输出。

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
	w := myApp.NewWindow("转换")

	f := binding.NewFloat()
	str := binding.FloatToString(f)
	short := binding.FloatToStringWithFormat(f, "%0.0f%%")
	f.Set(25.0)

	w.SetContent(container.NewVBox(
		widget.NewSliderWithData(0, 100.0, f),
		widget.NewLabelWithData(str),
		widget.NewLabelWithData(short),
	))

	w.ShowAndRun()
}
```

最后，在本节中，我们将查看[list](/docs/07-binding/04-list)数据。
