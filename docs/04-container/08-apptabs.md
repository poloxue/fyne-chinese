---
title: "08. Tab 布局 AppTabs"
weight: 8
---

# Tab 布局 AppTabs

AppTabs 容器用于允许用户在不同的内容面板之间切换。标签页要么只有文本，要么是文本和图标。建议不要混合使用一些标签页有图标而另一些没有图标的情况。使用 `container.NewAppTabs(...)` 创建标签容器，并传递 `container.TabItem` 项（可以使用 `container.NewTabItem(...)` 创建）。

可以通过设置标签的位置来配置标签容器，位置选项包括 `container.TabLocationTop`、`container.TabLocationBottom`、`container.TabLocationLeading` 和 `container.TabLocationTrailing`。默认位置是顶部。

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	//"fyne.io/fyne/v2/theme"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("TabContainer 控件")

	tabs := container.NewAppTabs(
		container.NewTabItem("标签 1", widget.NewLabel("你好")),
		container.NewTabItem("标签 2", widget.NewLabel("世界！")),
	)

	//tabs.Append(container.NewTabItemWithIcon("首页", theme.HomeIcon(), widget.NewLabel("首页标签")))

	tabs.SetTabLocation(container.TabLocationLeading)

	myWindow.SetContent(tabs)
	myWindow.ShowAndRun()
}
```

在移动设备上加载时，可能会忽略标签位置。在纵向方向，前导或尾随位置将被更改为底部。在横向方向，顶部或底部位置将移至前导。
