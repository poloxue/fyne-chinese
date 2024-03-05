---
title: "01. 几何 Geometry"
weight: 1
---

# 几何 Geometry

Fyne 应用基于每个窗口有一个画布。每个画布有一个根 CanvasObject，它可以是一个单独的控件或一个容器，用于控制多个子对象的大小和位置，这些子对象由布局控制。

### 位置

每个画布的原点位于左上角（0, 0），UI 的每个元素都可能根据输出设备进行缩放，因此 API 不描述像素或精确的尺寸。
例如，在120DPI的显示器上，位置（10, 10）可能从原点向右和向下各10像素，但在HiDPI（或“Retina”）显示器上，这可能更接近20像素。

每个 CanvasObject 引用的位置都是相对于它的父级的。这对于布局算法很重要，但对于开发者在例如 `Tappable.Tapped(PointEvent)` 处理程序这样的情况下也很重要。这里的 X/Y 坐标将从按钮的左上角而不是整个画布计算。这样设计是为了让代码尽可能自包含。

### 像素大小

像其他基于矢量的 GUI 库一样，Fyne 坐标需要基于某种基线显示器分辨率。所有[缩放](/docs/09-architecture/02-scaling)都是相对于这个值的。对于 Fyne 来说，该分辨率是120DPI。这意味着当你的显示器是120DPI且所有缩放值都设置为1时，`fyne.Size`中引用的尺寸将是1=1px。对于 HiDPI 屏幕，如上所述，实际 DPI 可能更接近240，在移动设备上甚至可能是360或更高。为了管理这种复杂性，工具包在内部管理缩放，因此你的应用总是看起来大小合适。如果用户设置的缩放比例较小，那么他们的应用将始终具有小于正常的字体、按钮等，当他们指定较大时，你的应用将适当放大。

与 [Material Design](https://material.io) 相比，我们可以看到他们的基线 DPI 是 [160](https://material.io/design/layout/pixel-density.html#pixel-density-on-android)，尽管数学上相似，但实际数字会有所不同。这意味着 Fyne 中的设备独立尺寸使用较小的数字来代表相同的物理尺寸。例如，Fyne 中高度为 `18` 的图标在标准的 Material Design（例如 Android）应用中的尺寸为 `24`。构建应用程序时，这并不重要，但在与设计师或熟悉 Material Design 的专家合作时可能很重要。

如果你开始加载位图图像，像素尺寸将变得重要。通常这些图像会适当缩放，但如果你指定 `FillMode=fyne.FillOriginal`，则由于像素密度的不同，实际图像大小在不同设备上会有所不同。通常这个功能会在 `Scroll` 容器内使用。Fyne 还定义了一个 `canvas.Raster` 原始类型，它将在输出设备的像素密度下精确绘制像素。这使你的代码能够在不了解运行设备的详细信息的情况下，以最高可能的输出分辨率进行绘制。如果由于某种原因你需要“像素完美”定位，你需要将 `CanvasObject.Size()` 乘以 `Canvas.Scale()`。