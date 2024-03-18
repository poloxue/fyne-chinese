---
title: "02. 创建第一个应用"
weight: 2
---

# 第一个应用

在完成了入门安装文档中的步骤后，你现在已经准备好构建你的第一个应用程序了。为了说明这个过程，我们将构建一个简单的“Hello World”应用程序。

一个简单的应用程序从使用`app.New()`创建一个应用实例开始，然后使用`app.NewWindow()`打开一个窗口。接着定义一个控件树，并使用窗口上的`SetContent()`将其设置为主内容。然后通过在窗口上调用`ShowAndRun()`来显示应用UI。

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello World")

	w.SetContent(widget.NewLabel("Hello World!"))
	w.ShowAndRun()
}
```

上面的代码可以使用命令`go build .`进行构建，然后通过运行hello命令或双击图标来执行。你也可以跳过编译步骤，直接使用`go run ..`来运行代码。

无论采取哪种方法，都会显示一个窗口，看起来像这样：

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/started/hello-dark.png)

如果你更喜欢浅色主题，只需设置环境变量`FYNE_THEME=light`，你就会得到：

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/started/hello-light.png)

这就是入门的全部内容了。要了解更多，你可以阅读完整的 [API文档](https://docs.fyne.io/api)。

