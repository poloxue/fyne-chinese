---
title: "03. 运行 Fyne Demo"
weight: 3
---

# 运行 Fyne Demo

如果你想在开始编写自己的应用程序之前看到Fyne工具包的实际效果，你可以查看我们的演示应用程序。

### 运行

如果愿意，你可以使用以下命令直接运行演示（需要Go 1.16或更高版本）：

```bash
go run fyne.io/fyne/v2/cmd/fyne_demo@latest
```

效果图：

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/started/fynedemo-dark.png)

对于早期版本的Go，你需要使用以下命令：

```bash
go run fyne.io/fyne/v2/cmd/fyne_demo
```

通过浏览应用的不同标签，你可以看到Fyne工具包的所有功能。

### 安装

你可以将该应用安装为计算机上的图形应用程序，就像所有其他应用程序一样。我们有一个有用的`fyne`工具可以为你完成这项工作。首先，你需要安装该工具：

```bash
go install fyne.io/fyne/v2/cmd/fyne@latest
```

之后，你可以简单地打包并安装演示应用程序：

```bash
fyne get fyne.io/fyne/v2/cmd/fyne_demo
```

完成这一步骤后，你可以在应用启动器中找到“Fyne Demo”。

### 探索代码

如果你对任何功能感兴趣，你应该查看源代码或加入社区频道之一。
