---
title: "12. 发布到应用商店"
weight: 12
---


# 分发到应用商店

按照[打包](/docs/01-started/08-packaging)页面所述打包图形应用程序会提供一个可以直接分享或分发的文件或捆绑包。然而，签名并上传到应用商店和市场是一个需要特定平台配置的额外步骤，我们将在这个页面中介绍。

在这些步骤中，我们将使用fyne命令行工具的一部分新工具。`fyne release`步骤处理为每个商店的签名和准备，但参数因平台而异，我们将在下面看到。

### macOS AppStore（自fyne 1.4.2起）

先决条件：

* 运行macOS和Xcode的Apple mac
* Apple开发者账户
* Mac AppStore 应用证书
* Mac AppStore 安装程序证书
* 从 AppStore 下载的 Apple Transporter 应用

1. 在[AppStore Connect](https://appstoreconnect.apple.com)上为要上传的构建准备好你的应用/版本。

2. 为发布捆绑完成的应用：

```bash
$ fyne release -appID com.example.myapp -appVersion 1.0 -appBuild 1 -category games
```

3. 将`.pkg`拖到Transporter上并点击“交付”。

4. 返回到AppStore Connect网站，选择你的构建版本进行发布，并提交审核。

### 谷歌Play商店（Android）

先决条件：

* Google Play控制台账户
* 分发密钥库（创建指南在
[android文档](https://developer.android.com/studio/publish/app-signing)）

1. 在[Google Play控制台](https://play.google.com/apps/publish)上为要上传的构建准备好你的应用/版本。关闭“Play应用签名”选项，因为我们自己管理它。

2. 为发布捆绑完成的应用：

```bash
$ fyne release -os android -appID com.example.myapp -appVersion 1.0 -appBuild 1
```

3. 将`.apk`文件拖到Play控制台中应用版本页面的构建投放区。

4. 开始新版本的推出。

### iOS AppStore（自fyne 1.4.1起）

先决条件：

* 运行macOS和Xcode的Apple mac
* Apple开发者账户
* iOS AppStore 分发证书
* 从 AppStore 下载的Apple Transporter应用

1. 在[AppStore Connect](https://appstoreconnect.apple.com)上为要上传的构建准备好你的应用/版本。

2. 为发布捆绑完成的应用：

```bash
$ fyne release -os ios -appID com.example.myapp -appVersion 1.0 -appBuild 1
```

3. 将`.ipa`拖到Transporter上并点击“交付”。

4. 返回到AppStore Connect网站，选择你的构建版本进行发布，并提交审核。
