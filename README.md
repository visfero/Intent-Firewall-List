<p align="center">
<img src="assets/firewalls-1529068049532.svg" alt="Intent Firewall List">
</p>
<h1 align="center">
Intent Firewall List
</h1>



> A List of The Firewall For Intent | Keep Rogue Applications Quiet



## Introduction 介绍

> ### IFW 是什么
>
> IFW 的全称为 `Intent Firewall` ，非官方中文名为 `意图防火墙`， 它于 Android 4.4.2 被引入到系统中，Google 没有提供官方 API 和文档来描述此功能，所以目前 IFW 是一个 Undocumented 的功能，它可能随时被更改。
>
> ### IFW 的功能
>
> Android 软件通过 Intent （意图） 来启动新活动、新服务等，而 IFW 的功能就是通过 XML 文件的配置，过滤 Intent ，让你不想要使其生效的 Intent 无效化（注意，这个 Intent 实际上还是被发送给系统了）。 
> IFW 是通过读取并解析存在于 `/data/system/ifw` 中的 XML 规则文件来进行规则过滤的，所有的配置是即时生效的。
>
> ### 限制
>
> IFW 仅能通过系统应用和 root 访问进行配置，这也是由于需要保证系统防火墙的配置安全。 
> IFW 在处理 Intent 时是**不考虑来源**的，它不去匹配这个 Intent 是来自于谁，它只关心当前 Intent 的去向和细节。
>
> ——摘自 [LetITFly BBS](https://bbs.letitfly.me/d/395) · [cubesky 立音](https://bbs.letitfly.me/u/18)



## Instructions 使用方法

> 1. 根据你要优化的应用的包名，在`Rules`文件夹下找到对于的文件夹，找到对应版本的文件夹。
> 2. 复制`[应用包名].xml`文件到你的安卓设备的`/data/system/ifw`文件夹下，IFW规则立即生效。



## Contribution 贡献

> ### 通过Github提交你的Rules
>
> 1. Fork 该仓库到一份自己的副本，在自己的副本内的 `Rules` 文件夹下，为需要制定`Rule`的应用新建 `[应用包名]` 文件夹，在`[应用包名]`文件夹内新建对应的`[应用版本号]`文件夹。
> 2. 在`[应用版本号]`目录下新建
>    - `Components.txt`文件 —— 该应用的所有组件
>    - `Rules.txt`文件 —— `Rule`禁用的所有组件
>    -  `Info.md`文件 —— `Rule`的详细说明
>    - `[应用包名].xml`文件 —— `Rule`本体
>
> 可一次编写多个应用，最后向我们打开一个 Pull request 即可。
>
> **格式可见 [RULES_FORMAT.md](https://github.com/LaelLuo/Intent-Firewall-List/blob/master/RULES_FORMAT.md)**

