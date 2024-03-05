---
title: "03. 树 Tree"
weight: 3
--- 

# 树 Tree

`Tree` 集合控件类似于 [List](/docs/06-collection/01-list) 控件（工具包的另一个集合控件），具有多级数据结构。像 `List` 一样，它旨在帮助构建性能良好的接口，以便在展示大量数据时使用。因此，控件不是用所有数据创建的，而是在需要时调用数据源。

`Tree` 使用回调函数在需要时请求数据。有四个主要的回调，`ChildUIDs`、`IsBranch`、`CreateNode` 和 `UpdateNode`。`ChildUIDs` 回调在这里传递每个子节点的唯一 ID 到请求的节点。这将以 `TreeNodeID` 为 `""` 被调用，首先获取所有显示在树根中的 ID 列表。`IsBranch` 回调应当在节点是分支时返回 `true`。如果节点 ID 有子节点，通常返回 `true` - 但你可以有一个空的分支。

**确保树中每个树节点的 id 是唯一的，这一点至关重要。**
例如，如果你正在构建一个文件管理器，ID 应该是文件路径而不是其名称。

其他两个回调与内容模板相关。

`CreateNode` 回调返回一个新的模板对象，就像列表一样，尽管有一个额外的 `bool` 参数，如果节点可以有子元素（是一个分支），则为 `true`。如前所述，`UpdateNode` 被调用以将数据应用于单元格模板。你应该根据 `TreeNodeID` 和 `isBranch` 参数更新内容。

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("树形控件")

	tree := widget.NewTree(
		func(id widget.TreeNodeID) []widget.TreeNodeID {
			switch id {
			case "":
				return []widget.TreeNodeID{"a", "b", "c"}
			case "a":
				return []widget.TreeNodeID{"a1", "a2"}
			}
			return []string{}
		},
		func(id widget.TreeNodeID) bool {
			return id == "" || id == "a"
		},
		func(branch bool) fyne.CanvasObject {
			if branch {
				return widget.NewLabel("分支模板")
			}
			return widget.NewLabel("叶子模板")
		},
		func(id widget.TreeNodeID, branch bool, o fyne.CanvasObject) {
			text := id
			if branch {
				text += " (分支)"
			}
			o.(*widget.Label).SetText(text)
		})

	myWindow.SetContent(tree)
	myWindow.ShowAndRun()
}
```
