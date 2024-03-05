---
title: "10. 在浏览器中运行"
weight: 10
---

# 在浏览器中运行

Fyne应用程序也可以通过标准的网络浏览器在网络上运行！由于不同引擎的标准和优势各异，这稍微复杂一些。

使用Fyne创建的网络应用将提供一个WASM运行时以及一个JavaScript代码包，这使得生成的网页可以查看当前浏览器并选择适合其优势的实现方式。这在大多数系统上提供了极好的用户体验。

为了准备你的应用通过网络使用，我们再次使用“fyne”命令行应用，它有一个用于快速测试的“serve”命令

```bash
go install fyne.io/fyne/v2/cmd/fyne@latest
fyne serve
```

你会看到，过了一会儿，一个网页服务器已经在8080端口启动。只需在你的网络浏览器中打开https://localhost:8080，你就可以使用你的应用了！

这个过程中使用的工具对Go版本非常敏感，因此可能会出现与版本不匹配相关的错误。如果你使用的是1.18版之后的Go，你应该确保你有1.18版的副本，并在你的环境中引用它，比如（对于一个基于[homebrew](https://brew.sh)的安装）：

```bash
export GOPHERJS_GOROOT=/opt/homebrew/Cellar/go@1.18/1.18.10/libexec
```

你可以在[GopherJS](https://github.com/gopherjs/gopherjs)文档上了解更多相关信息。

### 打包用于网络分发

`fyne serve`命令非常适合本地测试，但就像其他平台一样，你也会想要能够分发你的应用。为了准备上传的文件，就像常规的[打包](/docs/01-started/08-packaging)一样，使用`fyne package`命令。

```bash
fyne package -os web
```

你也可以选择只为WASM或JavaScript打包，而不是自动检测设置：

```bash
fyne package -os wasm
fyne package -os js
```

### 演示

你可以访问[demo.fyne.io](https://demo.fyne.io/)，在任何设备上测试Fyne应用的实际运行情况。

### 限制

截至v2.4.0版本发布，网络驱动程序还没有完全完成，所以你的应用可能无法使用以下功能：

* 多窗口（但对话框都可以在当前窗口内部工作）
* 文档和偏好设置的存储

这些问题正在被解决，并将在未来的版本中得到解决。
