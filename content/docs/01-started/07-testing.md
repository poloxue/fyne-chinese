---
title: "07. 测试 GUI 应用程序"
weight: 7
---

# 测试 GUI 应用程序

一个好的测试套件的一部分是能够快速编写测试并定期运行它们。Fyne的API旨在使应用程序测试变得简单。通过将组件逻辑与其渲染定义分离，我们可以在不实际显示它们的情况下加载应用程序，并完全测试其功能。

### 示例

我们可以通过扩展我们的[Hello World](/docs/01-started/02-hello)应用程序来演示单元测试，包括为用户输入他们的名字以便问候的空间。我们首先更新用户界面，使其包含两个元素：一个用于问候的`Label`和一个用于输入名字的`Entry`。我们使用`container.NewVBox`（一个垂直盒子容器）将它们一个接一个地显示。更新后的用户界面代码如下所示：

```go
func makeUI() (*widget.Label, *widget.Entry) {
	return widget.NewLabel("Hello world!"),
		widget.NewEntry()
}

func main() {
	a := app.New()
	w := a.NewWindow("Hello Person")

	w.SetContent(container.NewVBox(makeUI()))
	w.ShowAndRun()
}
```

为了测试这个输入行为，我们创建了一个新文件（以 `_test.go` 结尾，将其标记为测试），定义了一个`TestGreeter`函数。

```go
package main

import (
	"testing"
)

func TestGreeting(t *testing.T) {
}
```

我们可以添加一个验证初始状态的初始测试，为此我们测试从`makeUI`返回的`Label`的`Text`字段，如果它不正确，则错误测试。将以下代码添加到测试方法中：

```go
	out, in := makeUI()

	if out.Text != "Hello world!" {
		t.Error("Incorrect initial greeting")
	}
```

这个测试将通过 - 接下来我们添加到测试中以验证问候者。我们使用Fyne的`fyne.io/fyne/v2/test`包来帮助测试场景，调用`test.Type`来模拟用户输入。以下测试代码将检查当输入用户姓名时输出是否更新（也确保添加了导入）：

```go
	test.Type(in, "Andy")
	if out.Text != "Hello Andy!" {
		t.Error("Incorrect user greeting")
	}
```

你可以使用`go test .`运行所有这些测试 - 就像任何其他测试一样。这样做，你现在会看到一个失败 - 因为我们没有添加问候逻辑。将`makeUI`函数更新为以下代码：

```go
func makeUI() (*widget.Label, *widget.Entry) {
	out := widget.NewLabel("Hello world!")
	in := widget.NewEntry()

	in.OnChanged = func(content string) {
		out.SetText("Hello " + content + "!")
	}
	return out, in
}
```

这样做，你会看到测试现在通过了。你也可以运行完整的应用程序（使用`go run .`），并且当你在`Entry`字段中输入名字时，看到问候更新。还要注意，所有这些测试都是在不显示窗口或窃取你的鼠标的情况下运行的 - 这是Fyne单元测试设置的另一个好处。
