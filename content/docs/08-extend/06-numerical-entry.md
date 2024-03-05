---
title: "06. 数字输入框 Entry"
weight: 6
---

## 数字输入框 Entry

在传统意义上，GUI程序使用回调来自定义控件的操作。Fyne不暴露插入自定义回调来捕获控件上的事件，但这并不是必需的。Go语言完全有足够的扩展性来实现这一点。

我们可以简单地使用类型嵌入来扩展控件，使其只能输入数值。

首先创建一个新的类型结构体，我们将其称为`numericalEntry`。

```go
type numericalEntry struct {
    widget.Entry
}
```

如[扩展现有控件](https://developer.fyne.io/tutorial/extending-widgets)中所提到的，我们遵循良好实践并创建一个构造函数，该函数扩展了`BaseWidget`。

```go
func newNumericalEntry() *numericalEntry {
    entry := &numericalEntry{}
    entry.ExtendBaseWidget(entry)
    return entry
}
```

现在我们需要让条目只接受数字。这可以通过重写`TypedRune(rune)`方法来完成，这是`fyne.Focusable`接口的一部分。这将允许我们拦截按键输入的标准处理，并只通过我们想要的输入。在此方法中，我们将使用条件检查rune是否匹配0到9之间的任何数字。如果是，我们将其委托给嵌入式条目的标准`TypedRune(rune)`方法。如果不是，我们就忽略输入。此实现只允许输入整数，但如果需要，可以轻松扩展以检查将来的其他键。

```go
func (e *numericalEntry) TypedRune(r rune) {
	if r >= '0' && r <= '9' {
		e.Entry.TypedRune(r)
	}
}
```

如果我们想要更新实现以允许输入小数，我们可以简单地将`.`和`,`添加到允许的rune列表中（一些语言对于小数记数使用逗号而不是点）。

```go
func (e *numericalEntry) TypedRune(r rune) {
	if (r >= '0' && r <= '9') || r == '.' || r == ',' {
			e.Entry.TypedRune(r)
	}
}
```

通过这种方式，现在条目只允许用户在按键时输入数值。然而，粘贴快捷键仍然允许输入文本。为了解决这个问题，我们可以重写`TypedShortcut(fyne.Shortcut)`方法，这是`fyne.Shortcutable`接口的一部分。首先我们需要进行类型断言，检查给定的快捷键是否为`*fyne.ShortcutPaste`类型。如果不是，我们可以将快捷键委托回嵌入式条目。如果是，我们检查剪贴板内容是否为数值，通过使用`strconv.ParseFloat()`（如果你只想允许整数，`strconv.Atoi()`就足够了），然后如果剪贴板内容可以无误地解析，再将快捷键委托回嵌入式条目。

```go
func (e *numericalEntry) TypedShortcut(shortcut fyne.Shortcut) {
	paste, ok := shortcut.(*fyne.ShortcutPaste)
	if !ok {
		e.Entry.TypedShortcut(shortcut)
		return
	}

	content := paste.Clipboard.Content()
	if _, err := strconv.ParseFloat(content, 64); err == nil {
		e.Entry.TypedShortcut(shortcut)
	}
}
```

作为额外福利，我们还可以确保移动操作系统打开数值键盘而不是默认键盘。这可以通过首先导入`fyne.io/fyne/v2/driver/mobile`包并重写`mobile.Keyboardable`接口的`Keyboard() mobile.KeyboardType`方法来完成。在函数中，我们简单地返回`mobile.NumberKeyboard`类型。

```go
func (e *numericalEntry) Keyboard() mobile.KeyboardType {
	return mobile.NumberKeyboard
}
```

最后，结果代码可能如下所示：

```go
package main

import (
	"strconv"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/driver/mobile"
	"fyne.io/fyne/v2/widget"
)

type numericalEntry struct {
	widget.Entry
}

func newNumericalEntry() *numericalEntry {
	entry := &numericalEntry{}
	entry.ExtendBaseWidget(entry)
	return entry
}

func (e *numericalEntry) TypedRune(r rune) {
	if (r >= '0' && r <= '9') || r == '.' || r == ',' {
		e.Entry.TypedRune(r)
	}
}

func (e *numericalEntry) TypedShortcut(shortcut fyne.Shortcut) {
	paste, ok := shortcut.(*fyne.ShortcutPaste)
	if !ok {
		e.Entry.TypedShortcut(shortcut)
		return
	}

	content := paste.Clipboard.Content()
	if _, err := strconv.ParseFloat(content, 64); err == nil {
		e.Entry.TypedShortcut(shortcut)
	}
}

func (e *numericalEntry) Keyboard() mobile.KeyboardType {
	return mobile.NumberKeyboard
}

func main() {
	a := app.New()
	w := a.NewWindow("Numerical")

	entry := newNumericalEntry()

	w.SetContent(entry)
	w.ShowAndRun()
}
```

这个示例展示了如何扩展Fyne的`Entry`控件来创建一个只接受数值输入的`Entry`控件，通过重写`TypedRune`和`TypedShortcut`方法，并通过重写`Keyboard`方法为移动设备提供了数值键盘。
