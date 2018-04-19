# Carthage-的使用实例以及教程
* 介绍：Carthage类似于cocoapods，是一个第三方库框架管理工具。
* 特点：不会自动修改项目文件和生成配置，把对项目结构和设置的控制权交给用户，需要用户自行配置。
* 原理：自动将第三方框架编程为Dynamic framework(动态库)
* 限制：仅支持iOS8.0+，不能用来针对iOS8以前的系统版本进行开发
Carthage和cocoapods区别

    * cocoapods的项目是高度集中的，而carthage更灵活强调尽可能将任务委托给Xcode和Git
    * cocoapods在使用中会自动创建和更新workspace、依赖和Pod项目并进行整合
    * Carthage在使用中不需要创建和继承相应的workspace和project，只需要依赖打包好的framework文件即可
    * cocoapods相对来说功能要比Carthage多很多，因此也更复杂，而Cocoapods配置简单项目干净
    * Cocoapods有一个中心仓库，而Carthage是去中心化的，没有中心服务器也就避免了可能因中心节点错误而带来的失败，即Carthage每次配置和更新环境，只会去更新具体的库，时间更快
    * 想让自己的第三方库支持Carthage比让其支持cocoapods更加的简单
    * Carthage存在的一些缺陷
        * 库依然不如CocoaPods丰富
        * 仅支持iOS8+
        * 在使用第三方库的过程中无法查看源码总结：

cocoapods的方法更容易使用，而Carthage更灵活且对项目没有侵入性


Carthage安装

* 直接下载Carthage.pkg安装包，安装运行
* 如果使用的Xcode7.0+版本，那么可以使用下面的方法来安装
     *  安装home-brew
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
     * 升级brew
$ brew update
     * 使用brew来安装
$ brew install Carthage
![image](https://github.com/cq1402272764/Carthage/blob/master/Res/0.png)

* 查看版本
$ Carthage version
Carthage使用

1、命令创建
* 先进入到项目所在的文件夹
$ cd ~/Path/Project
* 创建一个空的Carthage文件
$ touch Cartfile
* 编辑cartfile文件，例如要安装AFN框架
git "https://github.com/AFNetworking/AFNetworking.git"
* 保存并关闭cartfile文件，使用cartfile安装框架
$ Carthage update --platform iOS
* 打开Carthage查看生成的文件目录
$ open Carthage

2、文件目录说明：
* || Carthage／Checkouts目录：从github获取的源代码
* || Carthage／Build目录：编译出来的Framework二进制代码库

3、配置项目：
* 打开项目，点击Target -> Build Phases -> Link Library with Libraries选择Carthage/Build目录中导入的framework
* 添加编译的脚本（该脚本文件保证在提交归档时会对相关文件和dSYMs进行复制）
1）点击Build Phases，点击“+” -> New Run Script Phase
![image](https://github.com/cq1402272764/Carthage/blob/master/Res/1.png)


2）添加脚本
/usr/local/bin/Carthage copy-frameworks
3）添加“Input Files”     $(SRCROOT)/Carthage/Build/iOS/AFNetworking.framework
![image](https://github.com/cq1402272764/Carthage/blob/master/Res/2.png)



4、在项目中使用第三方库
#import <AFNetworking/AFNetworking.h>

卸载Carthage
* 卸载Carthage：$ brew uninstall Carthage
* 更新第三方框架：
* 更新多个框架：修改Carfile文件，并从新执行 $ Carthage update
* 更新某个框架：$ Carthage update 具体的框架名称
* Carthage的工作过程说明
* ① 创建一个Cartfile文件，在该文件中列出您想使用的框架
* ② 运行Carthage，获取并编译Cartfile文件中列出的框架
* ③ 把框架的二进制文件配置到项目中

