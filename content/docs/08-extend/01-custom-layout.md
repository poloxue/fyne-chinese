---
title: "01. 自定义布局 Layout"
weight: 1
---

## 自定义布局 Layout

在Fyne应用程序中，每个`Container`都使用一个简单的布局算法来排列其子元素。Fyne在`fyne.io/fyne/v2/layout`包中定义了许多可用的布局。如果你查看代码，你会看到它们都实现了`Layout`接口。

```go
type Layout interface {
    Layout([]CanvasObject, Size)
    MinSize(objects []CanvasObject) Size
}
```

任何应用程序都可以提供一个自定义布局来以非标准的方式排列控件。为此，你需要在自己的代码中实现上述接口。为了说明这一点，我们将创建一个新的布局，该布局将元素排列在对角线上，并排列到其容器的左下角。

首先，我们将定义一个新类型`diagonal`，并定义其最小大小将是多少。为了计算这个，我们只需添加所有子元素（指定为`MinSize`的`[]fyne.CanvasObject`参数）的宽度和高度。

```go
import "fyne.io/fyne/v2"

type diagonal struct {
}

func (d *diagonal) MinSize(objects []fyne.CanvasObject) fyne.Size {
    w, h := float32(0), float32(0)
    for _, o := range objects {
        childSize := o.MinSize()

        w += childSize.Width
        h += childSize.Height
    }
    return fyne.NewSize(w, h)
}
```

对这个类型，我们添加一个`Layout()`函数，该函数应该将所有指定的对象移动到第二个参数中指定的`fyne.Size`中。

在我们的实现中，我们计算控件的左上角位置（这是`0` x参数，并且有一个y位置，即容器的高度减去所有子项高度的总和）。从顶部位置开始，我们简单地将每个项目位置按前一个子项目的大小向前移动。

```go
func (d *diagonal) Layout(objects []fyne.CanvasObject, containerSize fyne.Size) {
    pos := fyne.NewPos(0, containerSize.Height - d.MinSize(objects).Height)
    for _, o := range objects {
        size := o.MinSize()
        o.Resize(size)
        o.Move(pos)

        pos = pos.Add(fyne.NewPos(size.Width, size.Height))
    }
}
```

创建自定义布局就是这么简单。现在代码都写好了，我们可以将其作为`container.New`的`layout`参数使用。下面的代码设置了3个`Label`控件，并将它们与我们新的布局放在一个容器中。如果你运行这个应用程序，你将看到对角线控件的排列，并且在调整窗口大小时，它们将对齐到可用空间的左下角。

```go
package main

import (
    "fyne.io/fyne/v2"
    "fyne.io/fyne/v2/app"
    "fyne.io/fyne/v2/container"
    "fyne.io/fyne/v2/widget"
)

func main() {
    a := app.New()
    w := a.NewWindow("Diagonal")

    text1 := widget.NewLabel("topleft")
    text2 := widget.NewLabel("Middle Label")
    text3 := widget.NewLabel("bottomright")

    w.SetContent(container.New(&diagonal{}, text1, text2, text3))
    w.ShowAndRun()
}
```
