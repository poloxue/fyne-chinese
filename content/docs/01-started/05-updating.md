---
title: "05. 更新 GUI 内容"
weight: 5
---

# 更新 GUI 内容

在完成了Hello World教程或其他示例之后，你将创建一个基本的用户界面。在这个页面中，我们将看到如何从代码中更新GUI的内容。

第一步是将你想要更新的控件赋值给一个变量。在Hello World教程中，我们直接将`widget.NewLabel`传递给`SetContent()`，为了更新它，我们将其更改为两行不同的代码，例如：

```go
clock := widget.NewLabel("")
w.SetContent(clock)
```

一旦内容被赋值给一个变量，我们就可以调用像`SetText("new text")`这样的函数。在我们的示例中，我们将使用`Time.Format`的帮助，将标签的内容设置为当前时间。

```go
formatted := time.Now().Format("Time: 03:04:05")
clock.SetText(formatted)
```

这就是我们需要做的，以改变一个可见项的内容（见下面的完整代码）。然而，我们可以进一步定期更新内容。

### 在后台运行

大多数应用程序都需要在后台运行进程，例如下载数据或响应事件。为了模拟这一点，我们将扩展上述代码，使其每秒运行一次。

像大多数Go代码一样，我们可以创建一个goroutine（使用`go`关键字）并在那里运行我们的代码。如果我们将文本更新代码移动到一个新函数中，它可以在初始显示以及定期更新时被调用。通过组合goroutine和`time.Tick`在一个`for`循环中，我们可以每秒更新标签。

```go
go func() {
    for range time.Tick(time.Second) {
        updateTime(clock)
    }
}()
```

将这段代码放在`ShowAndRun`或`Run`调用之前是很重要的，因为它们在应用程序关闭之前不会返回。将所有这些结合在一起，代码将运行并每秒更新用户界面，创建一个基本的时钟控件。完整的代码如下：

```go
package main

import (
    "time"

    "fyne.io/fyne/v2/app"
    "fyne.io/fyne/v2/widget"
)

func updateTime(clock *widget.Label) {
    formatted := time.Now().Format("Time: 03:04:05")
    clock.SetText(formatted)
}

func main() {
    a := app.New()
    w := a.NewWindow("Clock")

    clock := widget.NewLabel("")
    updateTime(clock)

    w.SetContent(clock)
    go func() {
        for range time.Tick(time.Second) {
            updateTime(clock)
        }
    }()
    w.ShowAndRun()
}
```

这段代码演示了如何在Fyne应用程序中创建动态更新的内容，这是构建交云动用户界面的基础。
