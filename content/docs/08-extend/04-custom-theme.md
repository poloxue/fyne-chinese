---
title: "04. 自定义主题 Theme"
weight: 4
---

## 自定义主题 Theme

应用程序能够加载自定义主题，这些主题可以对标准主题进行小的更改，或提供完全独特的外观。一个主题需要实现`fyne.Theme`接口的函数，该接口定义如下：

```go
type Theme interface {
    Color(ThemeColorName, ThemeVariant) color.Color
    Font(TextStyle) Resource
    Icon(ThemeIconName) Resource
    Size(ThemeSizeName) float32
}
```

要应用我们的主题更改，我们首先定义一个实现了这个接口的新类型。

### 定义你的主题

我们从定义一个将成为我们主题的新类型开始，一个简单的空结构体就可以了：

```go
type myTheme struct {}
```

断言我们实现了一个接口是个好主意，这样编译错误会更接近于定义类型。

```go
var _ fyne.Theme = (*myTheme)(nil)
```

此时你可能会看到编译错误，因为我们还需要实现方法，我们从颜色开始。

#### 自定义颜色

`Theme`接口中定义的`Color`函数要求我们定义一个命名颜色，并且还为用户期望的变体提供了提示（例如`theme.VariantLight`或`theme.VariantDark`）。在我们的主题中，我们将返回一个自定义的背景颜色 - 对于明亮和暗黑主题使用不同的值。

```go
// 需要从"image/color"导入color包。

func (m myTheme) Color(name fyne.ThemeColorName, variant fyne.ThemeVariant) color.Color {
    if name == theme.ColorNameBackground {
        if variant == theme.VariantLight {
            return color.White
        }
        return color.Black
    }

    return theme.DefaultTheme().Color(name, variant)
}
```

你会看到这里的最后一行引用了`theme.DefaultTheme()`来查找标准值。这允许我们提供自定义值，但在我们不想提供自己的值时回退到标准主题。

当然，颜色比资源更简单，我们来看看如何自定义图标。

#### 覆盖默认图标

图标（和字体）使用`fyne.Resource`作为值，而不是像`int`（用于大小）或`color.Color`（用于颜色）这样的简单类型。我们可以使用`fyne.NewStaticResource`构建自己的资源，或者你可以传入使用[资源嵌入](https://developer.fyne.io/tutorial/bundle)创建的值。

```go
func (m myTheme) Icon(name fyne.ThemeIconName) fyne.Resource {
    if name == theme.IconNameHome {
        return fyne.NewStaticResource("myHome", homeBytes)
    }
    
    return theme.DefaultTheme().Icon(name)
}
```

如上所述，如果我们不想提供特定的覆盖，我们返回默认主题图标。

### 加载主题

在你可以加载主题之前，你还需要实现`Size`和`Font`方法。如果你满意使用默认值，你可以使用这些空实现。

```go
func (m myTheme) Font(style fyne.TextStyle) fyne.Resource {
    return theme.DefaultTheme().Font(style)
}

func (m myTheme) Size(name fyne.ThemeSizeName) float32 {
    return theme.DefaultTheme().Size(name)
}
```

要为你的应用设置主题，你需要添加以下代码行：

```go
app.Settings().SetTheme(&myTheme{})
```

通过这些更改，你可以应用自己的风格，进行小的调整或提供完全自定义的应用程序外观！
