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
> ### 基础格式
>
> ```xml
> <rules>
>   <[component] block="[true/false]" log="[true/false]" >
>     <intent-filter >
>       <action name="[action]" />
>     </intent-filter>
>   </[component]>
> </rules>
> ```
>
> 注意 IFW 只解析 `<rules/>` 标签下的 `<activity/>` `<service/>` `<broadcast/>` 标签
>
> ### 形象点说？
>
> `程序 A` 想要启动 `程序 B` 的某个服务，这个服务的名字为 `b` （毒瘤们常干的事）。 
> 这时候 `程序 A` 就会创建一个 `Intent` ，并在其中声明，我想要启动 `程序 B` 的 `b` 服务，然后通过上下文的 `startService` 或者 `startActivity` 将这个请求发送给系统。 
> 系统接收到请求后，先解析这个请求，知道它的目标是想要打开什么，然后传入 IFW 防火墙中，这时 IFW 防火墙读取自己目录下的规则列表并进行匹配，如果匹配到了相关的规则，则进行处理（默认通行，或者默认禁止）
> 如果是一个通行规则，或者没有该项的规则，则这个 Intent 被放过，相关服务或者活动被启动。
> 如果是一个阻挡规则，则这个 Intent 被丢弃，不会向下传递，目标应用程序不会被打开，但这个时候，系统返回给 `程序 A`的信息是：这个 Intent 是有效的，我找到了相关的程序并进行发送（如果真的没有相关程序会报找不到目标的错误）。
> 由于 Intent 已经发给了系统，而 `程序 A` 是信任系统的 ~~（废话，不信任就别干了）~~ ，所以他会认为这个 Intent 已经成功启动了。
> 不过注意，如果有些软件在发送 Intent 后去检查有没有成功开启服务的，它就会发现它想要的服务没有被启动，如果这时候 `程序 A` 反复的发送 Intent 要求启动程序则反而会导致系统资源的消耗和设备耗电量的增加。 
> IFW 不会禁用软件本身的接收器或者服务，所以你无法从 MAT 等软件中看到组件被禁用。
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
> **格式可见 RULES_FORMAT.md**

