---
title: "04. App 和 RunLoop"
weight: 4
---

# App 和 RunLoop

对于一个图形用户界面（GUI）应用程序来说，它需要运行一个事件循环（有时被称为运行循环），来处理用户交互和绘图事件。在Fyne中，这是通过使用`App.Run()`或`Window.ShowAndRun()`函数启动的。这些函数中的一个必须在你的`main()`函数的设置代码末尾被调用。

一个应用程序应该只有一个运行循环，因此你应该在代码中只调用`Run()`一次。第二次调用它将会导致错误。

```go
package main

import (
	"fmt"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("Hello")
	myWindow.SetContent(widget.NewLabel("Hello"))

	myWindow.Show()
	myApp.Run()
	tidyUp()
}

func tidyUp() {
	fmt.Println("Exited")
}
```

对于桌面运行时，一个应用程序可以通过调用`App.Quit()`直接退出（移动应用不支持此功能）- 通常在开发者代码中不需要。一旦所有窗口都被关闭，应用程序也将退出。另外，请注意，在应用程序退出之前，执行`Run()`之后的函数将不会被调用。
