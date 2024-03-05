---
title: "03. 资源包 Bundle"
weight: 3
---

## 资源包

基于 Go 的应用程序通常构建为单个二进制可执行文件，Fyne应用程序也是如此。单个文件使我们更容易分发和安装软件。不幸的是，GUI应用程序通常需要额外的资源来渲染用户界面。为了管理这个挑战，Go应用程序可以将资产捆绑到二进制文件本身中。Fyne工具包更喜欢使用"fyne bundle"，因为它有我们将在下面探索的各种好处。

捆绑资产的基本方法是执行"fyne bundle"命令。这个工具有各种参数来自定义输出，但在其最基本的形式中，要捆绑的文件将被转换为可以构建到您的应用程序中的Go源代码。

```bash
$ ls
image.png	main.go
$ fyne bundle -o bundled.go image.png
$ ls
bundled.go	image.png	main.go
$ 
```

`bundled.go`的内容将是我们然后可以在代码中访问的资源变量列表。例如，上面的代码将导致包含以下内容的文件：

```go
var resourceImagePng = &fyne.StaticResource{
	StaticName: "image.png",
	StaticContent: []byte{
...
	}}
```

如你所见，默认命名为"resource\<Name\>.\<Ext\>"。这个文件中使用的名称和包可以在命令参数中自定义。然后我们可以使用这个名称来，例如，在我们的画布上加载一张图片：

```go
img := canvas.NewImageFromResource(resourceImagePng)
```

Fyne资源只是一个带有唯一名称的字节集合，所以这可以是一个字体、一个声音
