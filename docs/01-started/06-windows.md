---
title: "06. 窗口 Window 处理"
weight: 6
---

# 窗口 Window 处理

窗口是使用`App.NewWindow()`创建的，并需要使用`Show()`函数来显示。`fyne.Window`上的辅助方法`ShowAndRun()`允许你同时显示窗口并运行应用程序。

默认情况下，窗口将通过检查`MinSize()`函数（在后面的示例中会有更多介绍）来显示其内容的正确大小。你可以通过调用`Window.Resize()`方法来设置更大的尺寸。这个方法接受一个`fyne.Size`，其中包含使用设备独立像素（这意味着在不同设备上将是相同的）的宽度和高度，例如，要默认使窗口正方形，我们可以这样做：

```go
w.Resize(fyne.NewSize(100, 100))
```

请注意，桌面环境可能有限制，导致窗口小于请求的尺寸。移动设备通常会忽略这一点，因为它们只以全屏显示。

如果你希望显示第二个窗口，你只需调用`Show()`函数。如果你想在应用程序启动时打开多个窗口，将`Window.Show()`与`App.Run()`分开也可能是有帮助的。下面的示例展示了如何在启动时加载两个窗口。

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello World")

	w.SetContent(widget.NewLabel("Hello World!"))
	w.Show()

	w2 := a.NewWindow("Larger")
	w2.SetContent(widget.NewLabel("More content"))
	w2.Resize(fyne.NewSize(100, 100))
	w2.Show()

	a.Run()
}
```

上述应用程序将在两个窗口都关闭时退出。如果你的应用程序安排得当，一个窗口是主窗口，其他窗口是辅助视图，你可以设置一个窗口为“主窗口”，这样如果该窗口关闭，应用程序就会退出。要做到这一点，使用`Window`上的`SetMaster()`函数。

窗口可以在任何时候被创建，我们可以改变上面的代码，使得第二个窗口（w2）的内容是一个打开新窗口的按钮。你也可以从更复杂的工作流中加载窗口，但要小心，因为新窗口通常会出现在当前活动内容之上。

```go
w2.SetContent(widget.NewButton("Open new", func() {
	w3 := a.NewWindow("Third")
	w3.SetContent(widget.NewLabel("Third"))
	w3.Show()
}))
```

这段描述说明了如何在Fyne应用程序中处理窗口，包括创建、显示、调整大小以及如何从代码中动态添加新窗口。
