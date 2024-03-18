---
title: "09. 系统托盘菜单"
weight: 9
---

# 添加系统托盘菜单

自 v2.2.0 版本以来，Fyne 内置了对系统托盘菜单的支持。此功能在 macOS、Windows 和 Linux 计算机上显示一个图标，当点击时，会弹出由应用程序指定的菜单。

由于这是一个特定于桌面的功能，我们首先必须进行运行时检查，以确认应用程序正在桌面模式下运行。为此，我们进行 Go 类型断言以获取对桌面功能的引用：

```go
	if desk, ok := a.(desktop.App); ok {
...
	}
```

如果 `ok` 变量为真，则我们可以使用标准 Fyne 菜单 API 设置菜单，你可能之前在 `Window.SetMainMenu` 中使用过这个 API。

```go
		m := fyne.NewMenu("MyApp",
			fyne.NewMenuItem("Show", func() {
				log.Println("点击了显示")
			}))
		desk.SetSystemTrayMenu(m)
```

将此代码添加到应用程序的设置中，运行应用程序，你会看到系统托盘中显示了一个 Fyne 图标。当你点击它时，会出现一个包含“显示”和“退出”的菜单。

默认图标是 Fyne 标志，你可以通过[应用元数据](/docs/01-started/11-metadata)更改这个设置，或者通过 `App.SetIcon` 或直接使用 `desk.SetSystemTrayIcon` 为系统托盘设置应用图标。

## 管理窗口生命周期

默认情况下，当你关闭所有窗口时 Fyne 应用将会退出，这可能不是你希望的系统托盘应用的行为。要覆盖此行为，你可以使用 `Window.SetCloseIntercept` 功能来覆盖窗口关闭时的操作。在下面的示例中，我们通过调用 `Window.Hide()` 来隐藏窗口而不是关闭它。在第一次显示窗口之前添加这个。

```go
	w.SetCloseIntercept(func() {
		w.Hide()
	})
```

隐藏窗口的好处是你可以简单地再次使用 `Window.Show()` 显示它，如果需要第二次使用相同的内容，这比创建一个新窗口更高效。我们更新之前创建的菜单以显示上面隐藏的窗口。

```go
	fyne.NewMenuItem("Show", func() {
		w.Show()
	}))
```

## 完整的应用程序

这就是使用 Fyne 设置系统托盘菜单的全部内容！本教程的完整代码如下所示。

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/driver/desktop"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("SysTray")

	if desk, ok := a.(desktop.App); ok {
		m := fyne.NewMenu("MyApp",
			fyne.NewMenuItem("Show", func() {
				w.Show()
			}))
		desk.SetSystemTrayMenu(m)
	}

	w.SetContent(widget.NewLabel("Fyne 系统托盘"))
	w.SetCloseIntercept(func() {
		w.Hide()
	})
	w.ShowAndRun()
}
```
