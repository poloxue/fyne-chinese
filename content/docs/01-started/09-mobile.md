---
title: "09. 打包移动应用"
weight: 9
---

# 打包移动应用

你的Fyne应用代码可以直接作为移动应用运行，就像它在桌面上做的那样。然而，将代码打包用于分发就复杂一些。这个页面将探索正是为了做到这一点而将你的应用带到iOS和Android上的过程。

首先，你需要为移动打包安装更多的开发工具。对于Android构建，你必须安装Android SDK和NDK，并设置适当的环境，以便工具（如`adb`）可以在命令行中找到。要构建iOS应用，你需要在你的macOS电脑上安装Xcode以及命令行工具可选包。

一旦你有了一个工作的开发环境，打包就很简单了。要为Android和iOS构建应用程序，以下命令将为你完成所有操作。确保有一个唯一的应用程序标识符，因为在你首次发布后更改这些是不明智的。

```bash
fyne package -os android -appID com.example.myapp -icon mobileIcon.png
fyne package -os ios -appID com.example.myapp -icon mobileIcon.png
```

在这些命令完成后（首次编译可能需要一些时间），你将在你的目录中看到两个新文件，`myapp.apk`和`myapp.app`。你会看到后者与darwin应用程序捆绑包同名 - 不要将它们混淆，因为它们在另一个平台上不会工作。

要在你的手机或模拟器上安装Android应用，只需调用：

```bash
adb install myapp.apk
```

对于iOS，要在设备上安装，打开Xcode并在“Window”菜单中选择“Devices and Simulators”菜单项。然后找到你的手机并将`myapp.app`图标拖到你的应用列表上。

如果你想在模拟器上安装，请确保使用`iossimulator`而不是`ios`打包你的应用程序

```bash
fyne package -os iossimulator -appID com.example.myapp -icon mobileIcon.png
```

之后，你可以如下使用命令行工具：

```bash
xcrun simctl install booted myapp.app
```

这些步骤介绍了如何为iOS和Android设备打包和安装Fyne应用程序，从而使Fyne成为开发跨平台移动应用的强大工具。
