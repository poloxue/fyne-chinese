---
title: "05. 扩展控件 Widget"
weight: 5
---

## 扩展控件 Widget

Fyne标准控件提供最小的功能和自定义选项以支持大多数用例。在某些时候可能需要更高级的功能。与其让开发者构建自己的控件，不如扩展现有的控件。

例如，我们将扩展图标控件以支持被点击。为此，我们声明一个新的结构体，嵌入了`widget.Icon`类型。我们创建一个构造函数，调用重要的`ExtendBaseWidget`函数。

```go
import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/widget"
)

type tappableIcon struct {
	widget.Icon
}

func newTappableIcon(res fyne.Resource) *tappableIcon {
	icon := &tappableIcon{}
	icon.ExtendBaseWidget(icon)
	icon.SetResource(res)

	return icon
}
```

> **注意：** 像`widget.NewIcon`这样的控件构造函数可能不适用于扩展，因为它已经调用了`ExtendBaseWidget`。

然后，我们添加新函数以实现`fyne.Tappable`接口，有了这些函数，每次用户点击我们的新图标时都会调用新的`Tapped`函数。接口需要有两个函数，`Tapped(*PointEvent)`和`TappedSecondary(*PointEvent)`，所以我们将添加这两个。

```go
import "log"

func (t *tappableIcon) Tapped(_ *fyne.PointEvent) {
	log.Println("I have been tapped")
}

func (t *tappableIcon) TappedSecondary(_ *fyne.PointEvent) {
}
```

我们可以使用如下简单的应用程序测试这个新控件。

```go
import (
    "fyne.io/fyne/v2/app"
    "fyne.io/fyne/v2/theme"
)

func main() {
	a := app.New()
	w := a.NewWindow("Tappable")
	w.SetContent(newTappableIcon(theme.FyneLogo()))
	w.ShowAndRun()
}
```
