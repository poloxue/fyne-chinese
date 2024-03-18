---
title: "06. 进度条 ProgressBar"
weight: 6
---

# 进度条 ProgressBar

进度条控件有两种形式，标准进度条向用户显示已达到的 `Value`，从 `Min` 到 `Max`。默认最小值是 `0.0`，最大值默认为 `1.0`。要使用默认值，只需调用 `widget.NewProgressBar()`。创建后，你可以设置 `Value` 字段。

要设置自定义范围，你可以手动设置 `Min` 和 `Max` 字段。标签将始终显示完成百分比。

进度控件的另一种形式是无限进度条。此版本仅通过将条的一部分从左向右移动然后再移动回来，简单地显示一些活动正在进行中。使用 `widget.NewProgressBarInfinite()` 创建此版本，并且一旦显示就会开始动画。

```go
package main

import (
	"time"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	myApp := app.New()
	myWindow := myApp.NewWindow("进度条控件")

	progress := widget.NewProgressBar()
	infinite := widget.NewProgressBarInfinite()

	go func() {
		for i := 0.0; i <= 1.0; i += 0.1 {
			time.Sleep(time.Millisecond * 250)
			progress.SetValue(i)
		}
	}()

	myWindow.SetContent(container.NewVBox(progress, infinite))
	myWindow.ShowAndRun()
}
```
