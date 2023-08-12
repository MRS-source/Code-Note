---
created: 2023-08-12T10:40:40.245Z
modified: 2023-08-12T15:21:14.599Z
---
Activity是用于给用户进行交互的用户界面组件

新建Android项目：

- 在New Project里可以选择带有各类内置模板，选择No Activity可以生成干净的项目
- Name表示项目名称
- Package name表示项目的包名（Android通过包名来区分不同应用程序的，因此包名一定要具有唯一性）
- Save location表示项目代码存放的位置
- Language默认选择Kotlin
- Minimum API默认选择API 24
- Build configuration language默认选择Kotlin DSL

项目构造：

- app目录存放代码、资源等内容，主要开发也在此
- app/libs目录存放第三方jar包，放在此目录下的jar包会被自动添加到项目的构建路径里
- app/src/main/java/com.xxx.xxx目录存放主要的代码
- app/src/main/res目录存放图片、布局、字符串等资源
- app/src/main/AndroidManifest.xml整个项目的配置文件

新建Activity页面：

- com.xxx.xxx目录右键→New→Activity→Empty Views Activity
- 勾选Generate Layout File会自动为该Activity创建一个对应的布局文件
- 勾选Launcher Activity会自动将该Activity设置为当前项目的主Activity
- 项目中的任何Activity都应该重写onCreate()方法，一般Android Studio会自动帮我们完成

创建和加载布局：

- 最好每一个Activity都能对应一个布局。布局是用来显示界面内容
