---
title: "01. 列表 List"
weight: 1
---

# 列表 List

`List` 集合控件是工具包中的集合控件之一。这些控件旨在帮助构建在呈现大量数据时性能非常高的界面。你还可以看到具有类似 API 的 [Table](/docs/06-collection/02-table) 和 [Tree](/docs/06-collection/03-tree) 控件。由于这种设计，它们使用起来稍微复杂一些。

`List` 使用回调函数来在需要数据时请求数据。有三个主要的回调函数：`Length`、`CreateItem` 和 `UpdateItem`。`Length` 回调（首先传递）是最简单的，它返回要展示的数据中有多少项。其他回调与模板相关 - 如何创建、缓存和重用图形元素。

`CreateItem` 回调返回一个新的模板对象。当控件呈现时，这将使用真实数据重新使用。此对象的 `MinSize` 将影响 `List` 的最小尺寸。最后，`UpdateItem` 被调用来将一个数据项应用于缓存的模板。使用这个来设置准备显示的内容。

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

var data = []string{"a", "string", "list"}

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("列表控件")

	list := widget.NewList(
		func() int {
			return len(data)
		},
		func() fyne.CanvasObject {
			return widget.NewLabel("template")
		},
		func(i widget.ListItemID, o fyne.CanvasObject) {
			o.(*widget.Label).SetText(data[i])
		})

	myWindow.SetContent(list)
	myWindow.ShowAndRun()
}
```
