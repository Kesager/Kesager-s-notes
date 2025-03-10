# Hallo World

基础概念：

Android Studio
- Google 基于 Jetbrains IntenlliJ IDEA Commutity Edition 开发的

Android SDK （Android Software Development Kit, 即android软件开发工具包）
- SDK版本有和相应的安卓版本

NDK（Native Development Kit）

gradle

AVD

安卓模拟器

Activity（活动）

# 创建第一个应用

在 Android Studio 中选择创建新项目，使用模板“Empty Activity”

一个应用的包名在Android中是唯一的，写法是域名反写（如本站域名 sager.eu.org 写作 org.eu.sager）。

创建完成后可点击标题栏处的运行按钮让应用在AVD上运行

接下来我们分析项目的文件结构

选择左侧的文件资源管理器的标题栏，在弹出的菜单栏中选择“Android”可以看到一套明晰的文件结构：
```
app
|- manifests
	AndroidManifest.xml
|- kotlin+java
	|- <包名>
		|- ui
			MainActivity.kt
	|- <包名>(androidTest)    *测试用例*
	|- <包名>(test)    *测试用例*
|- res    *资源目录*
	|- layout 
		activity_main.xml
		...

Gradle Scripts
	build.gradle.kts
...
```

实际上的项目结构，我们可以切换为 Project 查看
~~~
<项目名称>
	|- .gradle
	|- .idea
	|- .kotlin
	|- app
		|- src
			|- main
				|- java
					|- <包名>
						|- ui
						MainActivity.kt
				|- res
					|- layout
						activity_main.xml
						...
				AndroidManifest.xml    *描述应用程序的基本信息*
		gradle.properties
		proguard-rules.pro    *指定代码混淆规则*
		...
	|- gradle
	.gitignore    *版本控制*
	build.gradle.kts
	gradle.properties
	...
~~~

我们看到 `AndroidManifest.xml` :
``` xml
<?xml version="1.0" encoding="utf-8"?>  
<manifest xmlns:android="http://schemas.android.com/apk/res/android"  
    xmlns:tools="http://schemas.android.com/tools" >  
  
    <application
        android:allowBackup="true"  
        ...
        <activity
            android:name=".MainActivity"  
            android:exported="true"  
            android:label="@string/app_name" >  
            <intent-filter>
				<action android:name="android.intent.action.MAIN" />  
                <category android:name="android.intent.category.LAUNCHER" /> 
            </intent-filter>
        </activity>    
    </application>  
</manifest>
```
其中的`<activity>...</activity>` 用于定义本应用的全部活动，我们刚刚运行程序后所看到的就是此活动。

观察 `.app/src/main` 下的内容:
```
|- java
	|- <包名>
		|- ui
		MainActivity.kt
```

观察 `./app/src/res` 下的内容:
```
res
	|- drawable    *图片资源*
	|- layout    *布局*
		activity_main.xml
		...
	|- mipmap    *图标*
	|- value    *设置字符串和颜色等*
	...
```

我们可以找到与此活动对应的文件，分别是 `MainActivity.kt` (处理逻辑) 和 `activity_main.xml` (处理视图)。

> [!NOTE] 没看见 layout 文件夹?
> 新版本中的空白文件模板仅通过 `MainActivity.kt` 实现页面的显示，~~不妨看看下一章的内容，创建一个带 `activity_main.xml` 的活动！~~

上面我们观察了与应用呈现直接相关的文件，下面我们看看和编译相关的 `build.gradle`文件。

