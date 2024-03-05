---
title: "06. 主题 Icon 小图标"
weight: 6
---

# 主题 Icon 小图标

以下每个图标都可以通过`theme`包作为一个函数获得。例如`theme.InfoIcon()`。

这些图标也可以通过使用`ThemeIconName`以及在实现了`fyne.Theme`的结构体上的`Icon`方法，通过它们的源图标名称获得。例如`theme.Icon(theme.IconNameInfo)`。

## 列表

{{< embedhtml "icons.html" >}}

## 使用其他颜色集

每个图标都可以作为特定主题颜色的源使用各种公共帮助方法：

* `NewDisabledThemedResource`
* `NewErrorThemedResource`
* `NewInvertedThemedResource`
* `NewPrimaryThemedResource`

默认情况下，所有图标都适应当前主题前景色，使用`NewThemedResource`，它使用主题前景色。所有图标都是SVG `width="24"`, `height="24"`。


