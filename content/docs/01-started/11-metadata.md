---
title: "11. 应用元数据 Metadata"
weight: 11
---

# 应用元数据 Metadata

自`fyne`命令v2.1.0版本发布以来，我们支持一个元数据文件，允许你在仓库中存储有关你的应用的信息。这个文件是可选的，但可以帮助避免在每个包和发布命令中记住特定的构建参数。

文件应该命名为`FyneApp.toml`，位于你运行`fyne`命令的目录中（通常是`main`包）。文件的内容如下：

```toml
Website = "https://example.com"

[Details]
Icon = "Icon.png"
Name = "My App"
ID = "com.example.app"
Version = "1.0.0"
Build = 1
```

文件的顶部部分是元数据，如果你将你的应用上传到https://apps.fyne.io列表页面时会使用，因此它是可选的。[Details]部分包含了其他应用商店和操作系统在发布过程中使用的有关你的应用的数据。如果找到了这个文件，fyne工具将会使用它，很多强制性的命令参数如果元数据存在则不是必需的。你仍然可以使用命令行参数覆盖这些值。
