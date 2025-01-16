---
title: macOS Minecraft 开服教程
date: 2025-01-16 23:00:00 +800
categories: [网络, 服务]
tags: [Minecraft]     # TAG names should always be lowercase
description: macOS Minecraft Server Tutorial.
pin: false
image:
  path: /assets/image/posts/macmcserver/minecraft.png
  alt: Minecraft
---

欢迎来到腰果数码，这里是幺幺，M芯片有着目前最强的单核性能和能耗比，是用于小型高性能服务器的不二之选，应上期视频观众要求，本教程会教大家如何在macOS运行我的世界服务端。

1. ## 下载Java

第一步当然是下载并安装java，这里推荐在最佳苹果开发者微软的网站下载，<br />
[https://learn.microsoft.com/zh-cn/java/openjdk/download](https://learn.microsoft.com/zh-cn/java/openjdk/download)  <br />

这里我列了一个表格，你可以根据你需要的MC版本选择对应的java版本


| MC版本        | Java版本  |
| --------------- | ----------- |
| ≤1.16.5      | 8         |
| 1.16.5        | 8、11、16 |
| 1.18.2-1.20.1 | 17        |
| ≥1.20.5      | 21        |

具体MC版本与Java相关内容详见<br />
<https://www.bilibili.com/opus/939387567592177669>

[微软的网站](https://learn.microsoft.com/zh-cn/java/openjdk/download)清晰地列出了各个版本的下载地址，不过这里没有java8，Arm版Java8需要从[java官网](https://www.java.com/zh-CN/download/)下载
这里以最新的JDK21为例，如果你是Intel芯片选择`X64`版本，Apple Silicon选择`AArch64`版本。

选择`pkg`后缀的安装包下载安装即可，如果你经常要玩不同的MC版本也可以都安装上，后面会讲如何切换服务端运行时的Java版本。

2. ## 下载服务端

第二步就是下载服务端核心，我们可以在[Minecraft官网](https://www.minecraft.net/zh-hans/download/server)、[第三方核心的官网](https://www.mohistmc.com/)、[第三方的镜像站](https://sync.mcsl.com.cn/)下载需要的核心

这里演示使用[fabric 1.20.4服务端](https://fabricmc.net/use/server/)。

3. ## 启动命令

下载好核心后，新建一个文件夹。
> **文件夹名字和路径不要有中文和全角字符**
{: .prompt-danger }

用文本编辑器新建一个文件，命名为run.sh，文本编辑器我推荐使用notepad--或vscode

将如下命令复制到文件中，在java这一行中可以设置最小和最大内存，确保你使用的服务端核心文件名和启动脚本中的相同。

```bash
cd "$( dirname "$0" )"
#定义目录为当前目录
export JAVA_HOME=/Library/Java/JavaVirtualMachines/microsoft-21.jdk/Contents/Home
#设置Java路径（如果需要）
java -Xms1G -Xmx4G -jar fabric-server-launch.jar --nogui
#以nogui模式启动Minecraft服务端
```

### 3.1 选择java版本

要想选择需要的java版本，打开终端，输入以下命令就可以查看系统中已安装的所有 Java 版本和路径

`/usr/libexec/java_home -V`

将获取到的`java路径`替换脚本中的`JAVA_HOME`参数即可
![java](/assets/image/posts/macmcserver/javaversion.png)
_在终端列出所以Java版本_

### 3.2 启动sh

这时在终端内，将sh文件拖入后回车即可运行服务端，如果你觉得这样比较麻烦

可以将文件后缀改为`.command`

使用`chmod`` +x`为脚本添加可执行权限（输入`chmod`` +x` 把文件拖入终端），就能直接用终端运行了

```bash
chmod +x 脚本文件名
```

### 3.3 配置eula文件

第一次启动时需要我们同意eula用户协议，打开`eula.txt`将`false`改为`true`即可。

启动脚本后，看到`Done`就表示已经启动成功了，如果你是正版登录，在客户端输入`127.0.0.1`就能测试你的服务器了。

### 3.4 设置server.properties

不过我们还需要进行一些自定义设置，输入`stop`关闭服务器，在`server.properties`文件可以配置服务器的基础设置，这里列几个常用的设置选项翻译，具体的设置方法可以参照[MC Wiki](https://zh.minecraft.wiki/w/Server.properties)。


| 原文                 | 中文         |
| :--------------------- | :------------- |
| difficulty           | 难度         |
| enable-command-block | 允许命令方块 |
| gamemode             | 游戏模式     |
| level-seed           | 地图种子     |
| max-players          | 最大玩家数   |
| motd                 | 服务器标题   |
| online-mode          | 正版验证     |
| pvp                  | PVP          |
| server-port          | 服务器端口号 |
| simulation-distance  | 模拟距离     |
| view-distance        | 最大视距     |

### 3.5 Mod安装注意事项

之后有关Mod安装这里就不多讲了，选择支持Mod的服务端核心后和客户端一样放到Mods就行了，这里说几个注意事项。

> 选择正确的API，下载时不要下错Fabric和Forge的Mod版本，别忘记下载Mod的API依赖。
{: .prompt-warning }

> 不要把客户端Mod装到服务端，一些Mod像是小地图，Sodium是客户端模组，在服务端装了就可能就会崩溃。
{: .prompt-warning }

> 不要一次装太多Mod，如果你Mod多最好分批次测试好后再加入，不然有冲突了不大好找。
{: .prompt-warning }

1. ## 内网穿透

### 4.1 端口映射

此时你自己和局域网内的设备都可以用局域网IP直接连接到你的服务器，但是互联网上的还不行，考虑到许多人可能没有公网IP，并且大家的网络环境和路由器品牌不同，这里就不讲怎么端口映射了，有兴趣的可以自行网上搜索教程，这里讲一下怎么用Sakurafrp进行内网穿透。

### 4.2 Sakurafrp

Sakurafrp官方教程：[https://doc.natfrp.com/launcher/usage.html](https://doc.natfrp.com/launcher/usage.html)

打开Sakurafrp官网后注册账号并进行实名验证，注意实名验证需要一块钱。

在服务-创建列表创建一个隧道，选择一个离你最近的节点，因为我们是Java版所以选择`TCP隧道`，设置隧道名，本地端口选择`25565`
将获取到的`java路径`替换脚本中的`JAVA_HOME`参数即可
![port](/assets/image/posts/macmcserver/port.png)
_在网页设置Sakurafrp端口_

设置好后，到`首页`复制访问密钥
![key](/assets/image/posts/macmcserver/key.png)
_在首页复制访问秘钥_

到服务-软件下载页面下载macOS启动器，根据你的CPU架构选择
![macfrplauncher](/assets/image/posts/macmcserver/macfrplauncher.png)
_下载界面_

打开DMG后将SakuraLauncher（早苗）拖入到应用目录安装
![frpinstall](/assets/image/posts/macmcserver/frpinstall.png)
_安装App_

启动后将刚才复制的密钥粘贴到登录账户点击登录，有需要的可以打开开机启动
![inputkey](/assets/image/posts/macmcserver/inputkey.png)
_在登录账户处输入访问秘钥_

在隧道列表打开隧道开关
![openfrp](/assets/image/posts/macmcserver/openfrp.png)
_打开隧道开关_

你的好友就能用日志里的这个地址正常访问你的服务器了。

> 不要忘记输入后面的`:端口号` 注意冒号为英语半角的`:`而不是中文全角的`：`
{: .prompt-warning }

![logip](/assets/image/posts/macmcserver/logip.png)
_如图处为好友联机需要输入的地址_