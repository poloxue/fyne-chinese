---
title: "10. 数据绑定"
weight: 10
---

# 数据绑定

数据绑定在 Fyne v2.0.0 中引入，使得将许多控件连接到随时间更新的数据源变得更加容易。`data/binding` 包提供了许多有用的绑定，可以管理应用中使用的大多数标准类型。数据绑定可以使用绑定 API 管理（例如 `NewString`），也可以连接到外部数据项（如 `BindInt(*int)`）。

支持绑定的控件通常有一个 `...WithData` 构造器，在创建控件时设置绑定。你也可以调用 `Bind()` 和 `Unbind()` 来管理现有控件的数据。以下示例展示了如何管理一个与简单的 `Label` 控件绑定的 `String` 数据项。

```go
package main

import (
	"time"

	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/data/binding"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")

	str := binding.NewString()
	go func() {
		dots := "....."
		for i := 5; i >= 0; i-- {
			str.Set("倒计时" + dots[:i])
			time.Sleep(time.Second)
		}
		str.Set("发射！")
	}()

	w.SetContent(widget.NewLabelWithData(str))
	w.ShowAndRun()
}
```

你可以在本站的[数据绑定](/docs/07-binding/)部分了解更多信息。
