---
title: "02. 表格 Table"
weight: 2
--- 

# 表格 Table

`Table`集合控件类似于[List](/docs/06-collection/01-list)控件（工具包的另一个集合控件），它具有二维索引。像`List`一样，这旨在帮助构建性能非常高的接口，当展示大量数据时。因此，控件不是用所有数据创建的，而是在需要时调用数据源。

`Table`使用回调函数在需要数据时请求数据。有3个主要的回调，`Length`、`CreateCell`和`UpdateCell`。`Length`回调（首先传递）是最简单的，它返回要展示的数据中有多少项，它返回的两个int分别代表行数和列数。其他两个与内容模板相关。

`CreateCell`回调返回一个新的模板对象，就像列表一样。不同之处在于`MinSize`将定义每个单元格的标准大小，以及表格的最小大小（它至少显示一个单元格）。如前所述，`UpdateCell`被调用来将数据应用于单元格模板。传入的索引是相同的`(row, col)`int对。

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

var data = [][]string{[]string{"左上角", "右上角"},
	[]string{"左下角", "右下角"}}

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("表格控件")

	list := widget.NewTable(
		func() (int, int) {
			return len(data), len(data[0])
		},
		func() fyne.CanvasObject {
			return widget.NewLabel("宽内容")
		},
		func(i widget.TableCellID, o fyne.CanvasObject) {
			o.(*widget.Label).SetText(data[i.Row][i.Col])
		})

	myWindow.SetContent(list)
	myWindow.ShowAndRun()
}
```
