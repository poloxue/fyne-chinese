---
title: "08. 动画 Animation"
weight: 8
---

# 动画 Animation

Fyne 包含一个动画框架，允许您在一段时间内平滑地过渡画布属性从一个值到另一个值。动画可以包含任何代码，这意味着可以管理任何类型的对象属性，但是内置了尺寸、位置和颜色的动画。

动画通常使用画布包的内置助手创建，例如 `NewSizeAnimation`，并在创建的动画上调用 `Start()`。您可以设置动画以重复或自动反转，如下所示。

首先让我们看看逐渐改变 `Rectangle` 填充颜色的颜色动画。在以下代码示例中，我们将矩形设置为窗口的内容，如之前的代码示例所做的那样。最大的不同是我们在显示窗口之前启动的动画。使用 `NewColorRGBAAnimation` 创建动画，它将在指定的 `red` 状态到 `blue` 状态之间过渡颜色通道，并将在指定的持续时间（2秒）内完成。

```go
package main

import (
	"image/color"
	"time"

	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
	"fyne.io/fyne/v2/container"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")

	obj := canvas.NewRectangle(color.Black)
	obj.Resize(fyne.NewSize(50, 50))
	w.SetContent(container.NewWithoutLayout(obj))

	red := color.NRGBA{R:0xff, A:0xff}
	blue := color.NRGBA{B:0xff, A:0xff}
	canvas.NewColorRGBAAnimation(red, blue, time.Second*2, func(c color.Color) {
		obj.FillColor = c
		canvas.Refresh(obj)
	}).Start()

	w.Resize(fyne.NewSize(250, 50))
	w.SetPadded(false)
	w.ShowAndRun()
}
```

也可以同时对多个属性进行动画处理。如果您仔细观察，您会看到我们将矩形添加到了没有布局的容器中——这意味着我们可以手动移动或调整对象的大小。让我们添加一个新的位置动画，它将在窗口中移动 `Rectangle`，并自动反转。

```go
move := canvas.NewPositionAnimation(fyne.NewPos(0, 0), fyne.NewPos(200, 0), time.Second, obj.Move)
move.AutoReverse = true
move.Start()
```

因为 `CanvasObject` 的 `Move()` 函数期望一个 `fyne.Position` 参数，位置动画回调也是如此，我们可以简单地传递方法名称而不是创建一个新函数。如果您在第一个动画下面添加上面的代码，您会看到对象在改变颜色的同时跨越窗口移动！
