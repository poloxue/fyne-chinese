---
title: "08. 打包桌面应用"
weight: 8
---

# 打包桌面应用

将图形应用程序打包以供分发可能会很复杂。图形应用程序通常有与它们关联的图标和元数据，以及集成到每个环境所需的特定格式。Windows可执行文件需要嵌入图标，macOS应用是捆绑包，在Linux中有各种应该安装的元数据文件。多麻烦啊！

幸运的是，“fyne”应用有一个“package”命令可以自动处理这一切。只需指定目标操作系统和任何所需的元数据（如图标），就会生成适当的包。对于.icns或.ico图标转换将自动完成，所以只需提供.png文件 :)。你需要做的就是已经为目标平台构建了应用程序...

```bash
go install fyne.io/fyne/v2/cmd/fyne@latest
fyne package -os darwin -icon myapp.png
```

如果你使用的是Go的旧版本（<1.16），你应该使用`go get`安装fyne

```bash
go get fyne.io/fyne/v2/cmd/fyne
fyne package -os darwin -icon myapp.png
```

将创建myapp.app，一个完整的捆绑结构，用于分发给macOS用户。然后你也可以为Linux和Windows版本构建...

```bash
fyne package -os linux -icon myapp.png
fyne package -os windows -icon myapp.png
```

这些命令将创建：

  * myapp.tar.gz，包含从usr/local/开始的文件夹结构，Linux用户可以将其展开到他们的系统根目录。
  * myapp.exe（在第二次构建后，这是Windows包所需的）将嵌入图标和应用元数据。

如果你只想在你的电脑上安装桌面应用程序，那么你可以使用有用的install子命令。例如，要将你当前的应用程序系统范围内安装，你可以简单地执行以下操作：

```bash
fyne install -icon myapp.png
```

所有这些命令也支持默认图标文件`Icon.png`，这样你就可以避免每次执行时键入参数。从Fyne 2.1开始，还有一个[元数据文件](/docs/01-started/11-metadata)，你可以为你的项目设置默认选项。

当然，如果你愿意，你仍然可以使用标准的Go工具运行你的应用程序。

