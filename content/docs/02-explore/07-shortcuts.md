---
title: "07. 快捷键"
weight: 7
---

# 快捷键

快捷键是可以通过键盘组合键或上下文菜单触发的常见任务。快捷键，很像键盘事件，可以附加到一个聚焦的元素上，或者在`Canvas`上注册，以便在`Window`中始终可用。

## 在Canvas中注册

有许多标准的快捷键定义（如`fyne.ShortcutCopy`），它们连接到标准键盘快捷键和右键菜单。添加新`Shortcut`的第一步是定义快捷键。对于大多数用途，这将是一个键盘触发的快捷键，这是一个桌面扩展。为此，我们使用`desktop.CustomShortcut`，例如，要使用Tab键和Control修饰符，你可能会做如下操作：

```go
	ctrlTab    := &desktop.CustomShortcut{KeyName: fyne.KeyTab, Modifier: fyne.KeyModifierControl}
	ctrlAltTab := &desktop.CustomShortcut{KeyName: fyne.KeyTab, Modifier: fyne.KeyModifierControl | fyne.KeyModifierAlt}
```

注意，这个快捷键可以重复使用，所以你可以将它附加到菜单或其他项上。在这个示例中，我们希望它始终可用，所以我们将其注册到我们窗口的`Canvas`上，如下所示：

```go
	ctrlTab := &desktop.CustomShortcut{KeyName: fyne.KeyTab, Modifier: fyne.KeyModifierControl}
	w.Canvas().AddShortcut(ctrlTab, func(shortcut fyne.Shortcut) {
		log.Println("我们按下了Ctrl+Tab")
	})
	w.Canvas().AddShortcut(ctrlAltTab, func(shortcut fyne.Shortcut) {
		log.Println("我们按下了Ctrl+Alt+Tab")
	})
```

如你所见，在这种方式注册快捷键有两个部分 - 传递快捷键定义以及回调函数。如果用户输入键盘快捷键，那么函数将被调用并打印输出。

快捷键只能与修饰键结合使用。为了响应没有修饰键的键盘输入，请使用`canvas.OnTypedRune`或`canvas.OnTypedKey`。

## 在输入框中添加快捷键

当当前项目聚焦时，让快捷键仅适用也是有帮助的。这种方法可以用于任何可聚焦的控件，并通过扩展该控件并添加`TypedShortcut`处理器来管理。这和添加键处理器很像，不同之处在于传入的值将是一个`fyne.Shortcut`。

```go
type myEntry struct {
	widget.Entry
}

func (m *myEntry) TypedShortcut(s fyne.Shortcut) {
	if _, ok := s.(*desktop.CustomShortcut); !ok {
		m.Entry.TypedShortcut(s)
		return
	}

	log.Println("输入了快捷键:", s)
}
```

从上面的摘录中你可以看到如何实现一个`TypedShortcut`处理器。在这个函数内部，你应该检查快捷键是否为之前使用的自定义类型。如果快捷键是标准的，调用原始快捷键处理器（如果控件有一个）是个好主意。
完成这些检查后，你可以将快捷键与你正在处理的各种类型进行比较（如果有多个）。
