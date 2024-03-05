---
title: "01. 安装指南"
weight: 1
---

# 安装指南

使用 Fyne 工具包构建跨平台应用程序非常简单，但在开始之前需要安装一些工具。如果您的计算机已经为Go开发设置好了，以下步骤可能不是必需的，但我们建议您阅读一下您操作系统的提示，以防万一。如果本教程后面的步骤出现问题，那么您应该重新检查以下的先决条件。

### 先决条件

Fyne需要3个基本元素：Go工具（至少版本1.12）、一个C编译器（用于与系统图形驱动连接）和一个系统图形驱动。根据您的操作系统，安装指令会有所不同，请选择下面适合您的选项卡查看安装指令。

请注意，这些步骤仅用于开发 - 您的Fyne应用不需要为最终用户安装任何设置或依赖！

{{< hint warning >}} **如下的 termux 是用于在 Android 设备上构建 Fyne 应用，无 PC 依赖。** {{< /hint >}} 

{{< tabs "prerequisites" >}}

{{< tab "Windows" >}} 

- 从[下载页面](https://golang.org/dl/)下载Go并按照说明安装
- 为Windows安装以下测试过的C编译器之一：
  - MSYS2配合MingW-w64 - [msys2.org](https://www.msys2.org/)
  - TDM-GCC - [tdm-gcc.tdragon.net](https://jmeubank.github.io/tdm-gcc/download/)
  - Cygwin - [cygwin.com](https://www.cygwin.com/)
- 在Windows上，您的图形驱动程序已经安装好了，但建议确保它们是最新的。

使用MSYS2（推荐）的安装步骤如下：

- 从[msys2.org](https://www.msys2.org/)安装MSYS2
- 安装完成后不要使用打开的MSYS终端
- 从开始菜单打开“MSYS2 MinGW 64位”
- 执行以下命令（如果询问安装选项，请确保选择“全部”）：

```bash
$ pacman -Syu
$ pacman -S git mingw-w64-x86_64-toolchain
```

- 您需要将 /c/Program\ Files/Go/bin和 ~/Go/bin 添加到您的 $PATH 中，对于MSYS2，您可以将以下命令粘贴到终端中：
```bash
$ echo "export PATH=\$PATH:/c/Program\ Files/Go/bin:~/Go/bin" >> ~/.bashrc
```

- 为了让编译器在其他终端上工作，您需要设置Windows的%PATH%变量，以便找到这些工具。进入“编辑系统环境变量”控制面板，点击“高级”，并将“C:\msys64\mingw64\bin”添加到路径列表中。

{{< /tab >}}
{{< tab "MacOS" >}} 

- 从[下载页面](https://golang.org/dl/)下载Go并按照说明进行安装。
- 从[Mac App Store](https://apps.apple.com/us/app/xcode/id497799835?mt=12)安装Xcode。
- 通过打开终端窗口并输入以下命令来设置Xcode命令行工具：`xcode-select --install`。
- 在macOS上，图形驱动程序将已经安装。

{{< /tab >}}

{{< tab "Linux" >}}  

- 您需要使用包管理器安装Go、gcc和图形库头文件，以下命令之一可能会起作用。
- Debian / Ubuntu: `sudo apt-get install golang gcc libgl1-mesa-dev xorg-dev`
- Fedora: `sudo dnf install golang gcc libXcursor-devel libXrandr-devel mesa-libGL-devel libXi-devel libXinerama-devel libXxf86vm-devel`
- Arch Linux: `sudo pacman -S go xorg-server-devel libxcursor libxrandr libxinerama libxi`
- Solus: `sudo eopkg it -c system.devel golang mesalib-devel libxrandr-devel libxcursor-devel libxi-devel libxinerama-devel`
- openSUSE: `sudo zypper install go gcc libXcursor-devel libXrandr-devel Mesa-libGL-devel libXi-devel libXinerama-devel libXxf86vm-devel`
- Void Linux: `sudo xbps-install -S go base-devel xorg-server-devel libXrandr-devel libXcursor-devel libXinerama-devel`

- Alpine Linux: `sudo apk add go gcc libxcursor-dev libxrandr-dev libxinerama-dev libxi-dev linux-headers mesa-dev`
- NixOS: `nix-shell -p libGL pkg-config xorg.libX11.dev xorg.libXcursor xorg.libXi xorg.libXinerama xorg.libXrandr xorg.libXxf86vm`

{{< /tab >}}

{{< tab "Raspberry Pi" >}} 

您需要使用包管理器安装Go、gcc和图形库头文件。

```bash
sudo apt-get install golang gcc libegl1-mesa-dev xorg-dev
```

{{< /tab >}}
{{< tab "BSD" >}} 

您需要使用包管理器安装Go、gcc和图形库头文件。

- FreeBSD: sudo pkg install go gcc xorg pkgconf
- OpenBSD: sudo pkg_add go
- NetBSD: sudo pkgin install go pkgconf

{{< /tab >}}
{{< tab "Android" >}} 

- 要为Android开发应用，您首先需要为您当前的电脑（Windows、macOS或Linux）安装工具。
- 完成后，您需要安装Android SDK和Android NDK——推荐的方法是安装[Android Studio](https://developer.android.com/studio/index.html)，然后转到Tools > SDK Manager，并从SDK Tools安装NDK（并行）包。
- 或者，您可以下载[Standalone Android NDK](https://github.com/android/ndk/wiki#supported-downloads)，这是一种更精简的方法。解压缩文件夹，并将ANDROID_NDK_HOME环境变量指向它。

{{< /tab >}}
{{< tab "IOS" >}} 
- 要为iOS开发应用，您将需要访问一台按照上面macOS标签配置的苹果Mac电脑。
- 您还需要创建一个苹果开发者账户并注册开发者计划（需要支付费用）以获取在任何设备上运行应用所需的证书。
{{< /tab >}}
{{< tab "Termux" >}} 

在Android上编译Fyne应用，您将需要Android 9或以上版本。

- 安装fdroid，然后从那里安装termux。
- 打开Termux并安装Go和Git：`pkg install golang git`。
- 从[https://github.com/Lzhiyong/termux-ndk](https://github.com/Lzhiyong/termux-ndk)安装NDK和SDK到termux，并设置环境变量`ANDROID_HOME`和`ANDROID_NDK_HOME`。

{{< /tab >}}

{{< /tabs >}}

### 下载

使用Go模块（Go 1.16及更高版本要求），在使用包之前需要设置模块。

#### Go模块（适用于Go 1.16或更新版本）

如果您不使用模块或您的模块已经初始化，可以跳过此步骤到下一个步骤。运行以下命令并将MODULE_NAME替换为您偏好的模块名（应在为您的应用程序专门创建的新文件夹中调用）。

```bash
$ cd myapp
$ go mod init MODULE_NAME
```

现在您需要下载Fyne模块和辅助工具。使用以下命令完成：

```bash
$ go get fyne.io/fyne/v2@latest
$ go install fyne.io/fyne/v2/cmd/fyne@latest
```

如果您不确定Go模块如何工作，考虑阅读[教程：创建一个Go模块]。

#### 旧版Go安装

使用旧版Go发布安装Fyne工具包和辅助工具，只需执行go get命令：

```bash
$ go get fyne.io/fyne/v2
$ go get fyne.io/fyne/v2/cmd/fyne
```

### 检查您的安装

在编写应用或运行示例之前，您可以使用Fyne安装工具检查您的安装。只需从链接下载适合您计算机的应用并运行它，您应该看到类似以下屏幕的内容：

![](https://cdn.jsdelivr.net/gh/poloxue/images@gofyne/started/setup.png)

如果您的安装有任何问题，请查看[故障排除](/docs/10-faq/03-troubleshoot) 部分以获取提示。

### 运行演示

如果您在开始编写自己的应用程序之前想看看Fyne工具包的实际运行情况，您可以通过执行以下命令在您的计算机上运行我们的演示应用：

```bash
$ go run fyne.io/fyne/v2/cmd/fyne_demo@latest
```

请注意，首次运行需要编译一些C代码，因此可能比平时需要更长的时间。后续构建会重用缓存，将会快得多。

#### 旧版 Go 版本

要在旧版Go上运行演示，只需执行以下命令：

```bash
$ go run fyne.io/fyne/v2/cmd/fyne_demo
```

### 安装

如果您愿意，您也可以使用以下命令安装演示（需要Go 1.16或更高版本）：

```bash
$ go install fyne.io/fyne/v2/cmd/fyne_demo@latest
```

对于早期版本的Go，您需要使用以下命令：

```bash
$ go get fyne.io/fyne/v2/cmd/fyne_demo
```

如果您的GOBIN环境变量已添加到路径中（在macOS和Windows上默认应该如此），那么您就可以运行演示了：

```bash
$ fyne_demo
```

就是这样！现在您可以用您选择的IDE编写自己的Fyne应用程序了。就这些了！现在你可以在你选择的IDE中编写自己的Fyne应用程序了。如果你想看到一些Fyne代码的实际运用，那么你可以阅读你的第一个应用程序。

