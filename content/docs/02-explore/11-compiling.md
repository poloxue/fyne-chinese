---
title: "11. 编译选项"
weight: 11
---

# 编译选项

Fyne 通常会通过选择驱动程序和配置来适当地为目标平台配置您的应用程序。以下构建标签得到支持，可帮助您的开发。例如，如果您希望在桌面计算机上模拟移动应用程序，您可以使用以下命令：

```sh
go run -tags mobile main.go
```

| 标签 | 描述 |
|----------|---------------------------|
| `debug`  | 显示调试信息，包括视觉布局，以帮助理解您的应用。 |
| `gles`   | 强制使用嵌入式 OpenGL (GLES) 而不是完整的 OpenGL。这通常由目标设备控制，通常不需要。 |
| `hints`  | 显示开发者提示以进行改进或优化。使用 `hints` 运行时，当您的应用程序不遵循材料设计或其他建议时，将记录下来。 |
| `mobile` | 此标签在模拟的移动窗口中运行应用程序。当您想要在不编译和安装到设备的情况下预览您的应用在移动平台上的外观时非常有用。 |
| `no_animations` | 禁用标准控件和容器中的非必要动画。 |
| `no_emoji` | 不包含嵌入的 emoji 字体。这将在您的应用中禁用 emoji，但会使二进制文件更小。 |
| `no_native_menus` | 此标志专门用于 macOS，表示应用程序不应使用 macOS 原生菜单。相反，菜单将在应用程序窗口内显示。在 macOS 上测试应用程序以模拟 Windows 或 Linux 上的行为时最有用。 |

