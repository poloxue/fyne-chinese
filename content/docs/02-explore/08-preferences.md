---
title: "08. 偏好设置"
weight: 8
---

# 偏好设置

为应用程序存储用户配置和值是应用开发者的常见任务，但在多个平台上实现它可能既乏味又耗时。为了简化这个过程，Fyne 提供了一个 API，用于以清晰且易于理解的方式在文件系统上存储值，同时为您处理复杂的部分。

让我们从 API 的设置开始。它是 [Preferences](https://pkg.go.dev/fyne.io/fyne/v2?tab=doc#Preferences) 接口的一部分，其中存在用于 Bool、Float、Int 和 String 值的存储和加载功能。它们每个都包含三个不同的函数，一个用于加载，一个带有回退值的加载，最后一个用于存储值。下面为 String 类型展示了这三个函数及其行为：

```go
// String 查找键的字符串值
String(key string) string
// StringWithFallback 查找字符串值，并在未找到时返回给定的回退值
StringWithFallback(key, fallback string) string
// SetString 为给定键保存一个字符串值
SetString(key string, value string)
```

这些函数可以通过创建的应用变量并调用其 `Preferences()` 方法来访问。请注意，创建带有唯一 ID 的应用是必要的（通常像反转的 url 那样）。这意味着应用程序需要使用 `app.NewWithID()` 来创建，以拥有自己存储值的位置。它大致可以像下面的示例那样使用：

```go
a := app.NewWithID("com.example.tutorial.preferences")
[...]
a.Preferences().SetBool("Boolean", true)
number := a.Preferences().IntWithFallback("ApplicationLuckyNumber", 21)
expression := a.Preferences().String("RegularExpression")
[...]
```

为了展示这一点，我们将构建一个简单的小应用，它总是在设定的时间后关闭。这个超时应该是用户可更改的，并在应用程序的下一次启动时应用。

让我们首先创建一个名为 `timeout` 的变量，用于以 `time.Duration` 的形式存储时间。

```go
var timeout time.Duration
```

然后，我们可以创建一个选择控件，让用户从几个预定义的字符串中选择超时，然后将超时乘以字符串所对应的秒数。最后，使用 `"AppTimeout"` 键将字符串值设置为选定的值。

```go
timeoutSelector := widget.NewSelect([]string{"10秒", "30秒", "1分钟"}, func(selected string) {
    switch selected {
    case "10秒":
        timeout = 10 * time.Second
    case "30秒":
        timeout = 30 * time.Second
    case "1分钟":
        timeout = time.Minute
    }

    a.Preferences().SetString("AppTimeout", selected)
})
```

现在，我们想要获取设置的值，如果不存在，我们想要有一个回退，将超时设置为最短的一个，以节省用户等待时的时间。这可以通过将 `timeoutSelector` 的选定值设置为加载的值或回退值（如果是这种情况）来完成。通过这种方式，选择控件中的代码将针对该特定值运行。

```go
timeoutSelector.SetSelected(a.Preferences().StringWithFallback("AppTimeout", "10秒"))
```

最后一部分将只是有一个函数，在一个单独的 goroutine 中启动，并在选定的超时后告诉应用退出。

```go
go func() {
    time.Sleep(timeout)
    a.Quit()
}()
```

最终，结果代码应该看起来像这样：

```go
package main

import (
    "time"

    "fyne.io/fyne/v2/app"
    "fyne.io/fyne/v2/widget"
)

func main() {
    a := app.NewWithID("com.example.tutorial.preferences")
    w := a.NewWindow("超时")

    var timeout time.Duration

    timeoutSelector := widget.NewSelect([]string{"10秒", "30秒", "1分钟"}, func(selected string) {
        switch selected {
        case "10秒":
            timeout = 10 * time.Second
        case "30秒":
            timeout = 30 * time.Second
        case "1分钟":
            timeout = time.Minute
        }

        a.Preferences().SetString("AppTimeout", selected)
    })

    timeoutSelector.SetSelected(a.Preferences().StringWithFallback("AppTimeout", "10秒"))

    go func() {
        time.Sleep(timeout)
        a.Quit()
    }()

    w.SetContent(timeoutSelector)
    w.ShowAndRun()
}
```

这段代码演示了如何利用 Fyne 的 Preferences API 来存储和读取用户的偏好设置，例如应用的超时设置。通过这种方式，开发者可以在多个平台上轻松地实现配置的存储和加载，而不需要处理底层的文件系统操作。Fyne 为处理复杂的部分提供了一个简单的界面，使得开发跨平台应用程序变得更加容易和直接。
