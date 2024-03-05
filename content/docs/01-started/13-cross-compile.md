---
title: "13. 跨平台编译"
weight: 13
---

## 跨平台编译

使用Go进行跨平台编译被设计得非常简单 - 我们只需设置目标操作系统的环境变量`GOOS`（如果目标是不同的架构，还需要设置`GOARCH`）。不幸的是，当使用原生图形调用时，Fyne中的CGo使用使这变得有些复杂。

### 从开发计算机编译

要跨编译Fyne应用程序，你还必须设置`CGO_ENABLED=1`，这告诉go启用C编译器（当目标平台与当前系统不同时，这通常是关闭的）。不幸的是，这意味着你必须为你将要编译的目标平台安装一个C编译器。安装适当的编译器后，你还需要设置`CC`环境变量来告诉Go使用哪个编译器。

安装所需工具有许多方法 - 并且可以使用不同的工具。Fyne开发者推荐的配置是：

| GOOS（目标） | CC | 提供者 | 下载 | 备注 |
|------|----|----------|----------|-------|
| `darwin`  | `o32-clang` | osxcross | [来自github.com](https://github.com/tpoechtrager/osxcross) | 你还需要安装macOS SDK（下载链接处有指引） |
| `windows` | `x86_64-w64-mingw64-gcc` | mingw64 | 包管理器 | 对于macOS使用[homebrew](https://brew.sh) |
| `linux`   | `gcc` 或 `x86_64-linux-musl-gcc` | gcc 或 musl-cross | [cygwin](https://www.cygwin.com/) 或 包管理器 | musl-cross可从[homebrew](https://brew.sh)获取，提供linux gcc。你还需要为编译安装X11和mesa头文件。 |

设置上述环境变量后，你应该能够以通常的方式进行编译。如果进一步出现错误，很可能是由于缺少包。一些目标平台需要安装额外的库或头文件才能成功编译。

### 使用虚拟环境

由于Linux系统能够轻松地交叉编译到macOS和Windows，因此当你不是从Linux开发时，使用虚拟化环境可能更简单。Docker镜像是复杂构建配置的有用工具，这也适用于Fyne。可以使用不同的工具。Fyne开发者推荐的工具是[fyne-cross](https://github.com/fyne-io/fyne-cross)。它受到[xgo](https://github.com/karalabe/xgo)的启发，并使用基于[golang-cross](https://github.com/docker/golang-cross)镜像构建的[docker镜像](https://hub.docker.com/r/fyneio/fyne-cross)，该镜像包括了Windows的MinGW编译器和macOS SDK，以及Fyne的需求。

fyne-cross允许为以下目标构建二进制文件并创建分发包：

| GOOS | GOARCH |
|------|----|
| darwin | amd64 |
| darwin | 386 |
| linux | amd64 |
| linux | 386 |
| linux | arm64 |
| linux | arm |
| windows | amd64 |
| windows | 386 |
| android | amd64 |
| android | 386 |
| android | arm64 |
| android | arm |
| ios | |
| freebsd | amd64 |
| freebsd | arm64 |

> 注意：iOS编译仅支持在darwin主机上。

#### 要求

- go >= 1.13
- docker

#### 安装

你可以使用以下命令安装`fyne-cross`（需要Go 1.16或更高版本）：

```bash
go install github.com/fyne-io/fyne-cross@latest
```

对于Go的早期版本，你需要使用以下命令代替：

```bash
go get github.com/fyne-io/fyne-cross
```

#### 使用方法

```bash
fyne-cross <command> [options]

命令包括：

	darwin        为darwin OS构建和打包fyne应用程序
	linux         为linux OS构建和打包fyne应用程序
	windows       为windows OS构建和打包fyne应用程序
	android       为android OS构建和打包fyne应用程序
	ios           为iOS OS构建和打包fyne应用程序
	freebsd       为freebsd OS构建和打包fyne应用程序
	version       打印fyne-cross版本信息

使用 "fyne-cross <command> -help" 获取有关命令的更多信息。
```

#### 通配符

`arch`标志支持通配符，以防你想要针对指定GOOS的所有支持GOARCH进行编译

示例：

```bash
fyne-cross windows -arch=*
```

等同于

```bash
fyne-cross windows -arch=amd64,386
```

#### 示例

以下示例交叉编译并打包[fyne示例应用程序](https://github.com/fyne-io/examples)

```bash
git clone https://github.com/fyne-io/examples.git
cd examples
```

##### 编译并打包主示例应用

```bash
fyne-cross linux
```

> 注意：默认情况下，fyne-cross将在当前目录下编译包。
>
> 上面的命令等同于：`fyne-cross linux .`

##### 编译并打包特定示例应用

```bash
fyne-cross linux -output bugs ./cmd/bugs
```

通过上述方法，使用`fyne-cross`可以轻松地为多个平台交叉编译和打包Fyne应用程序，而无需手动配置每个平台的复杂环境，从而简化了跨平台开发和分发过程。
