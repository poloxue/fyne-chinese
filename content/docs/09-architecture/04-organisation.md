---
title: "04. 包组织 Package"
weight: 4
---

# 包的组织

Fyne 项目分为许多包，每个包提供不同类型的功能，如下所示：

`fyne.io/fyne/v2`
: 这个导入提供了所有 Fyne 代码共有的基本定义，包括数据类型和接口。

`fyne.io/fyne/v2/app`
: app 包提供启动新应用的 API。
: 通常你只需要 `app.New()` 或 `app.NewWithID()`。

`fyne.io/fyne/v2/canvas`
: canvas 包提供 Fyne 中所有的绘图 API。
: 完整的 Fyne 工具包由这些原始图形类型组成。

`fyne.io/fyne/v2/container`
: container 包提供用于布局和组织应用的容器。

`fyne.io/fyne/v2/data/binding`
: binding 包包含将数据源绑定到控件的方法。

`fyne.io/fyne/v2/data/validation`
: validation 包提供工具用于验证控件内的数据。

`fyne.io/fyne/v2/dialog`
: dialog 包包含确认、错误和文件保存/打开等对话框。

`fyne.io/fyne/v2/layout`
: layout 包提供用于容器的各种布局实现（在后续教程中讨论）。

`fyne.io/fyne/v2/storage`
: storage 包提供存储访问和管理功能。

`fyne.io/fyne/v2/test`
: 使用 test 包内的工具可以更容易地测试应用。

`fyne.io/fyne/v2/widget`
: 大多数图形应用是使用一系列控件创建的。
: Fyne 中的所有控件和交互元素都在这个包中。
