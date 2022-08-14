# 准备

## 了解术语[^17]

**双清:** Dalvik/ART Cache Cache 其目的就是清除分区以及数据，简称重置手机。

**三清:** Dalvik/ART Cache Cache Data 刷机前基本上必选三清，目的是使新系统的兼容性达到最佳。

**四清:** Dalvik/ART Cache Cache Data System 四清针对版本差异过大的系统。
 
!!! warning  end

     重要！
     四清后不刷入系统无法开机进系统！！只能电脑刷或者储存卡刷。


**五清:** Dalvik/ART Cache Cache Data System Internal Storage（内置储存） 
!!! warning  end

    一旦选了这个清除，那手机内置存储上的东西就都没有了！就不能从手机选择卡刷包了！

**六清:** Dalvik/ART Cache Cache Data System.

**底包:**既不是ROM也不是OTA软件包，它是一组**低级驱动程序**，可帮助操作系统完成其想做的任何事情。 它包括调制解调器，蓝牙，引导程序，DSP等各种内容。支持所有Snapdragon和MTK设备，包括仅限中国的设备。底包就相当于一个纯净版或者内核版的系统包

**MTK**:联发科。
MTK和高通是生产手机CPU的厂家。MTK平台和高通平台指的是这两家的操作系统。

**A/B分区**

Android从7.0开始引入新的OTA升级方式，A/B System Updates，这里将其叫做A/B系统。顾名思义，A/B系统就是设备上有A和B两套可以工作的系统（用户数据只有一份，为两套系统共用），简单来讲，可以理解为一套系统分区，另外一套为备份分区。其系统版本可能一样；也可能不一样，其中一个是新版本，另外一个旧版本，通过升级，将旧版本也更新为新版本。当然，设备出厂时这两套系统肯定是一样的。之所以叫套，而不是个，是因为Android系统不是由一个分区组成，其系统包括boot分区的kernel和ramdisk，system和vendor分区的应用程序和库文件，以及userdata分区的数据

A/B系统实现了无缝升级(seamless updates)，有以下特点：出厂时设备上有两套可以正常工作的系统，升级时确保设备上始终有一个可以工作的系统，减少设备变砖的可能性，方便维修和售后。

!!! info  end

    OTA升级在Android系统的后台进行，所以更新过程中，用户可以正常使用设备，数据更新完成后，仅需要用户重启一次设备进入新系统。如果OTA升级失败，设备可以回退到升级前的旧系统，并且可以尝试再次更新升级。

**VAB架构**

又称虚拟AB分区，出厂安卓11的新机型，**几乎都是VAB架构**。

安卓分区架构发展史为：onlyA，AB，onlyA动态分区，AB动态分区，VAB架构。 所谓的VAB架构，其实就是AB分区，套上了动态分区，再解决了AB分区的空间占用问题。

刷机时经常会刷写的分区(system,vendor,boot,recovery等等)。userdata分区就是用户分区，格式化data就是格式化的这个分区。需要注意的是，格式化data和清空data，是两个不同的概念，经常会有小白把这两个概念搞混淆。

格式化data就是把userdata的分区进行格式化操作，就像你格式化U盘一样，是格式化操作。

而清空data，是删除data分区的所有文件及文件夹。当你遇到data挂载不上时，你清空data是没有效果的，这个时候，你需要进行格式化data操作，才能挂载data，所以，这两个不要搞混淆了

**通用系统映像(GSI/SGSI)**

[https://source.android.google.cn/devices/tech/ota/dynamic_partitions/implement](https://source.android.google.cn/devices/tech/ota/dynamic_partitions/implement)

从Android 9开始，Google更改了要求，所有设备都必须使用[system-as-root]

GSI则由A-only和A/B进行区分刷入

GSI则是一种可以忽略厂商定制的通用刷机包

**动态分区**

Google在Android 10开始引入了动态分区（Dynamic Partitions） 简单来说，就是把原来的system , vendor , product还有odm分区整合到了一起，构成super分区 在刷入设备的时候动态调整system等分区的大小

**什么是GSI**

GSI代表通用系统映像。这是一个文件系统映像，您可以将其刷到设备的系统分区。之所以具有通用性，是因为它使用新的标准化硬件API访问硬件（因此它可以在任何启用treble的设备上运行）。

**字库(分区)**

字库是硬件，就相当于电脑的硬盘。

功能机时代，很多手机程序、控制信息、字库信息是存储在一个专用芯片里面，芯片中主要部分是字库，所以一些售后和维修人员就习惯把这个存储芯片称做字库芯片。不过，到了智能机时代，这个存储芯片的功能已经远远超越了存储字库这么简单，所以它也远不是“字库”所能概括的，更准确的表述应该为eMMC芯片(embedded MultiMediaCard）。　

简单来说，“字库”(eMMC芯片)就相当于电脑中的BIOS+硬盘，一方面，它里面固化有手机的启动程序、基本输入输出程序、系统设置信息等等；另一方面，它还起到了存储照片、音乐等文件的作用，也就是我们经常提到的手机xxGB存储空间，而且手机的ROM(系统固件)也在这颗芯片当中，由此可见它对于一部手机的重要性。　

与手机一样，“字库”(eMMC芯片)也有相应的分类。

1、原装专用字库，即原厂生产、针对相应型号专门使用的芯片；

2、原装代用字库，同样是由生产，在原装字库货源短缺的情况下，替代原装字库使用的芯片，由于不是专门适用某型号机器的字库芯片，所以在体积上与原装字库存在差异，一般都要稍大一些；

3、其他品牌的字库，例如某芝部分型号的芯片，可以替换原装字库使用。

!!! tip "简单来说"
    字库要是坏了，换主板吧

**ROM包**
华为，小米，OPPO等都是安卓手机，但它们的系统又各不相同。这些系统本质上都是基于安卓系统的，他们对安卓系统进行定制，加入自己特有的服务。比如我们看到很多手机出厂就自带APP，这些就是 定制化之后的安卓系统 , 这些安卓系统就叫做ROM包。

**Recovery**

当手机系统文件被损坏从而不能正常启动时，我们可以进入recovery小系统对主体系统进行修复。

**第三方Recovery**

官方的recovery功能较少，一般可以清除缓存，擦除所有数据，刷入官方指定的系统，而不能刷第三方系统，所以就有人做 Recovery 去代替官方 (即第三方Recovery) 的，这样就能刷非官方的ROM了。

**FastbootD**

据我所知, fastbootd 是用户空间中的 fastboot。

在动态分区手机. `data`, `system`等原来的物理分区, 现在都被放到一个共同的`super`分区下. 这种"虚拟分区"只在用户空间(Android系统里)可见, 也就是说原版fastboot只能识别到整个`super`, 而`super`里的`data`这些却不行.

所以fastbootd 就是动态分区手机的 fastboot(指非动态分区手机的).

![a5nZlt.png](https://s1.328888.xyz/2022/08/13/TGOJ6.png)

[What is FastbootD? How to Boot to FastbootD Mode - DroidWin](https://www.droidwin.com/fastbootd-mode/)

## 了解刷机

### **深刷**

深刷就是底层刷机，顾名思义，这是一种从底层刷写手机分区的方式，与正常的程序相比，这种方式更为彻底，无视所有软件层面的权限，例如BL锁。

底层刷机模式常用于使用卡刷（Recovery下以及一系列使用ADB刷机方式的统称）或者线刷（Bootloader下使用Bootloader命令刷机的方式）刷成砖后救砖的场景下。按照主流处理器，高通为9008刷机模式，MTK为MTK PreLoader模式，海思麒麟为eRecovery模式（类rec操作）和eDownload模式。

!!! note
    MTK联发科芯片机型的深刷口被小mi提交修复，目前 天矶920 以后少有能使用此方法的。高通需要9008端口即可。详见刷机部分。

[底层相关刷机教程示例？](https://wiki.pchelper666.com/%E5%BA%95%E5%B1%82%E5%88%B7%E6%9C%BA%E6%95%99%E7%A8%8B)

### **OTA**

**这是升级，谈不上刷机**

OTA 意思就是**增量升级**，就是在原先系统的基础上增加新功能，也许是给手机打个补丁，也许是对性能的优化。**手机要活着能进系统且未修改才能用**。OTA 不会删除资料和系统的设定。备份资料放的位置要问官方，但通常不需要知道位置，内建备份也有还原功能，还能选择要还原的东西，还原的时候有问题的部分可以选择略过。

有些档案用 patch 的方式处理了, 有些用覆盖的方式 (要看做这个 OTA 包的人怎么做), 所以, 如果有档案与预期的不同 (通常是 root 后会删除或修改档案),  OTA 会失败。

你也可以解 OTA 的包进行修补获取Root权限。

### **软刷**

软件刷就是刷机大师，刷机精灵等的第三方刷机软件刷，现在已经绝迹了；

### **厂刷**

寄回厂子……


### **线刷**

线刷是 Fastboot 模式刷机。

线刷是用 Fastboot，一般都是直接刷镜像，由 uboot 以直接写入闪存的办法把镜像直接写到闪存对应的位置（或者说分区）。

线刷时备份资料可以使用PC端的程式来管理，出问题的话三清之后再选择性恢复，再不行就全部设定和资料重头来过。线刷 要有电脑, 执行特定的程式. (通常就算手机挂到都进不去 Recovery 也能刷)

所以线刷包实际一般就是包含了 Fastboot 程序和各个系统镜像以及一个可执行的脚本的包，用户直接运行那个脚本，脚本调用 Fastboot 来刷。

### **卡刷 /第三方 REC**

卡刷就是 Rcovery 模式刷机

!!! tip "Do you know?"
    区别卡刷包 和线刷包最明显的区别是 (卡刷包的文件内容）里有 **Recovery 文件，而（**线刷包的文件内容）里有 FLASH 文件，如果你注意到上方路径，从文件名可以看到线刷包文件名里有 “FASTBOOT” 。

一般是在 recovery 里进行的，有直接刷镜像的比如 kernel 部分，但像 system 都是挂载 system 分区后再个别的更新里面的文件（差分或者直接覆盖），而不是像线刷那样把整个 system 镜像重刷一次。如果是通过打二进制补丁差分更新的话（绝大部分官方 OTA 包的做法），就要求被更新的文件和出厂时一样，否则就会失败，这是 OTA 失败的原因。优点是比较简单快捷，非常适合不会刷机的新手。

具体卡刷应该分两种, 一种是**小的更新包** (作法与 OTA 一样, 当然结果也一样), 另一种是完整的系统包, 这种通常是把系统的 partition 重新 format 再把资料放上去. (不会动到使用者资料的分区)。

卡刷可以用手机直接下载卡刷包，更名Update.zip后进入recovery刷机，刷后资料还会在，但是通常不做资料清除的话很容易发生问题，严重的就是一直出现系统错误，轻的则是偶尔出现闪退。

所以基本上刷完机最好进Recovery三清，刷前做三清也行，重点就是该清的要清一清，不然问题很多。接着要还原备份的时候如果系统本差异太大最好不要还原系统设定和App之类的资料，还原一些使用者data就好。卡刷需要存储空间，一般能进 recovery 就能刷。

卡刷包有比较复杂些的目录结构，除了用来更新的文件外，也包括一个可执行文件和脚本，但这两个脚本是给recovery来用的，而不是用户。



!!! info  "**什么是第三方REC？？**"
    Recovery像是一个独立的微型系统，可以不依赖于安卓操作系统主体单独运行。Recovery的中文名是恢复，顾名思义，当手机系统文件被损坏从而不能正常启动时，我们可以进入recovery小系统对主体系统进行修复。可是官方的recovery功能较少，一般可以清除缓存，擦除所有数据，刷入官方指定的系统，而不能刷第三方系统，所以就有人做 Recovery 去代替官方 (即第三方Recovery) 的，这样就能刷非官方的ROM了。像是所有的官改包，第三方是配的包，国际版的包以及原生系统，都是用第三方REC刷入。可以说，有了第三方REC，是你刷机的出发点，想刷什么都可以（当然刷的东西兼容你的设备）有了它，你就可以各种不同的系统，开始真正的刷机之路。但是，大部分的第三方REC不支持OTA升级，也就是说，每次你收到系统更新的时候，都必须要下载完整包更新。





#### 第三方Recovery

第三方Recovery有很多种，最常用的是 `TWRP` ，还有很多基于 `TWRP` 修改的种类，比如 `橙狐Recovery`，`SHRP`，`PBRP`，`奇兔Recovery` 等等。

可以去 TWRP 官网 [Here](https://twrp.me/Devices/) 搜索，或者在 TWRP 官方APP下载，但是速度可能不是很好,也可以去[橙狐官网](https://orangefox.download/zh-CN)找。


如果以上途径都找不到，可以去酷安找你机型的话题，在话题内搜索关键词：`TWRP，rec，橙狐，oringe，pbrp，沥青，shrp。`


## 准备设备

---

本教程用到的工具我**已经打入附带的文件包** [^1]

### 提前注意

**安卓系统的版本需要是 5.0~12.0 之间 (2022)**

!!! warning "注意"
    **解锁BL或救砖都会让你的文件被清空，需要备份**


!!! warning "注意"
    - 解锁设备将允许修改系统重要组件，并有可能在一定程度上导致设备受损
    - 解锁后设备安全性将失去保证
    - 解锁后部分对系统安全性依赖高的功能和服务失效
    - 解锁后部分系统功能遭到修改后，将影响系统新版本升级
    - 解锁后由于刷机导致的硬件故障，售后维修网点可以按非保修处理
    - 三星设备解锁后会永久性熔断 KNOX 安全认证
    - 大部分手机的版权认证 DRM 等级也会从 L1 下降至 L3、无法通过 Play 商店认证等。

不建议你在主力机上解锁 Bootloader，而且，如果厂商明确表示不能解锁 Bootloader ，**请放弃**。如果一定要刷机并且报着变砖的觉悟，可以尝试**深刷**强解。

### 准备驱动文件

准备你的手机对应的机型的驱动文件，文件包提供 Vivo 和 Oppo 的两种驱动文件[1^]。
个人建议下载一个泛用型驱动 [universal adb drivers](https://adb.clockworkmod.com/)。少数情况下不能识别的话，需要我们用「手机厂商名 + adb driver」的关键词搜索得到相关的下载和安装教程。

安装完驱动请重启。 [相关手机驱动下载-FiimeROM](https://mi.fiime.cn/qudong)
[相关驱动站点](https://kamiui.ml/E52shuaji/)



!!! tip "**对于非深刷玩家如何检查是否链接？**"  
    💡 重启后在设备开机状态下连接电脑，打开终端，输入`adb devices`，如果返回了设备名称，说明 adb 配置完成；用 `adb reboot bootloader`进入 fastboot 界面（这步不适用fastbootd设备,即安卓十），键入 `fastboot reboot`后，若设备重启，说明 fastboot 正常。



### 准备设备和平台工具

Win7 或以上电脑一台，能传输文件的数据线一条（**最好是原装线**），电脑下载解压[安卓平台文件包](https://dl.google.com/android/repository/platform-tools_r33.0.2-windows.zip)或[Linux版本安卓平台工具包](https://dl.google.com/android/repository/platform-tools-latest-linux.zip)或[Mac版本](https://dl.google.com/android/repository/platform-tools-latest-darwin.zip)，退出所有手机助手类软件。

解压工具包，你会看到 adb 和 fastboot ，这是我们针对 Android 设备进行高级调试和安装的工具。

!!! tip "提示[^3]"
    如果你已经安装了 [choco](https://chocolatey.org/) 或 [homebrew](https://brew.sh/) 等包管理工具的话，Windows 输入`choco install adb universal adb-drivers -y`，Mac 输入 `brew install android-platform-tools`能最方便的完成 adb 和 fastboot 的配置。Windows 用户可以参照  [Windows 操作系统下的 ADB 环境配置](https://sspai.com/post/40471) 这篇文章；macOS 用户可以尝试  [此脚本](https://github.com/corbindavenport/nexus-tools) 或是参考 [使用 Mac 为 Android 手机刷原生系统](https://sspai.com/post/38535) 进行手动配置。最后最最不济，可以尝试在 Google  [开发者页面](https://developer.android.com/studio/releases/platform-tools?hl=zh-cn) 下载对应 adb 包，解压后在对应的目录下执行指令亦可，或者是尝试 [WebADB](https://app.webadb.com/#/) 或  [adb 在线执行器](https://adb.http.gs/) 这样的在线 adb 工具，比较考验浏览器的兼容性。

### 准备深度测试或申请解锁BL（深刷可跳过）

> BL 是 bootloader 的简称 就是 手机开机时，最先运行的小程序：开机引导程序 ，Bootloader 锁，主要是在引导过程中对系统签名，内核签名及 Recovery 签名进行检验，如果签名不一致，即终止引导。绿机器人儿用它来进行开机自检和初始化手机硬件，它会指引手机找到系统分区并启动操作系统，相当于电脑上的BIOS。
> 
厂商通常会对手机的bootloader上锁，这样它就只能运行厂商认证过的操作系统和recovery了。如果boatloader发现要运行的系统不是指定的系统，就会阻止它运行。

在开发者选项中打开「OEM 解锁」（除了少部分流入我国市场的国外运营商有锁机外，此选项基本都可供用户开启。）

!!! danger 
    **解bl锁会清除手机（恢复出厂设置）所有数据，记得提前备份好。**

不同的手机解锁方式不同，你甚至可以去线下店让服务人员解锁。或者从自己的社区中获取本机型的解锁信息。部分手机解锁很麻烦，比如华为，想要解锁只能去淘宝买解锁码，而且当你刷回官方 ROM 时，会自动加锁。当然，华为的解锁码是和硬件相关的，买到解锁码把它记下，下次进 FASTBOOOT 输入`fastboot oem unlock 解锁码`就可以了。

而对于小米手机，可以通过这个地址 [申请解锁](https://www.miui.com/unlock/download.html) 下载工具，然后打开手机设置，进入关于手机–>系统版本点10下，在`设备解锁状态`中绑定账号和设备，进入`Fastboot`模式(关机后，同时按住开机键和音量下键)，打开刚才下载的工具，点击 `解锁` 后系统会恢复出厂系统并解锁。也可以通过OEM解锁

**如果你的设备不能进行官方解锁，可以尝试深刷强解 。**

!!! note
    一些古董机型是没有BL锁的，比如红米Note。

附上[小米解锁教程](https://web.vip.miui.com/page/info/mio/mio/detail?postId=28646781&boardId=5415551&isComment=&isRecommend=0&app_version=dev.211029&ref=share).


### 准备获取文件




[FiimeROM-小米红米原生|移植|官改|SGSI|驱动|插件](https://mi.fiime.cn/Dtech/66.html)

这时候，你要确认手机已经解锁BL锁。

上述工具已经打入附带文件包。

**如果你是深刷玩家，请单独查看刷入节：深刷。**

### 备份完整分区[^15]

这里的分区就是字库。

什么是备份完整字库？我们说的64GB，128GB，256GB等等，这个就是说的主板的储存容量，也就是字库。某个分区的数据损坏，好听的说法是分区数据坏了，难听的说法是字库损坏了。

所以，解锁bl后第一件事，就是备份完整字库，以防不测。有人会说，不是有9008吗？有必要备份完整字库吗？有必要。

原因：假如一个手机所有分区加起来有100个，9008大概会刷写30个左右，剩下的70个不会刷写。

那么这个70个当中有某个分区数据损坏了，9008是无法救砖的，必须返厂，用工厂售后（非卖手机的那种售后）的工厂包，方可救砖。当然，如果这个工厂包，没有刷写完100个分区的话，基本上也是无法救砖的。

备份文件下载链接 [pan.baidu.com/s/1Yp3ljJWWvKMdpUpSUkt_Sw](http://pan.baidu.com/s/1Yp3ljJWWvKMdpUpSUkt_Sw) 提取码:vo15 ，或者我打包的文件中[^1],文件来自[^15]

**高通机型备份字库**

安装个MT管理器，使用root权限执行【高通字库备份.sh】即可。备份的文件在/sdcard/Rannki目录中。

**高通机型还原字库**

提前把之前备份好的Rannki文件夹，复制到 `/sdcard/Rannki`，安装个MT管理器，使用root权限执行【高通字库还原.sh】即可。

**MTK 机型备份字库**

安装个MT管理器，使用root权限执行【MTK字库备份.sh】即可。备份的文件在/sdcard/Rannki目录中。

**MTK 机型还原字库**

提前把之前备份好的Rannki文件夹，复制到 `/sdcard/Rannki`，安装个MT管理器，使用root权限执行【MTK 字库还原.sh】即可。

字库备份还原，解决的不只是基带问题，

是：除硬盘物理损坏外的所有问题，解决率为100％。

**以上如何防止掉基带教程由酷安 Rannki 原创**

??? note "详细叙述"
    
    
    **UFS闪存手机**
    
    主板一般被分成了6个硬盘，即**sda，sdb，sdc，sdd，sde，sdf。**
    
    所以，主板设备代码分别是：`/dev/block/sda，/dev/block/sde，/dev/block/sdc，/dev/block/sdd，/dev/block/sde，/dev/block/sdf`
    
    备份分区的代码举例：`dd if=/dev/block/sda1 of=/sdcard/1.img,dd if=/dev/block/sda2 of=/sdcard/2.img`等等等等............................
    
    还原分区的代码举例：`dd if=/sdcard/1.img of=/dev/block/sda1,dd if=/sdcard/2.img of=/dev/block/sda2` 等等等等............................
    
    **Emmc闪存手机**
    
    主板设备代码：**/dev/block/mmcblk0**
    
    备份分区的代码举例：`dd if=/dev/block/mmcblk0p1 of=/sdcard/1.img,dd if=/dev/block/mmcblk0p2 of=/sdcard/2.img`等等等等............................
    
    还原分区的代码举例：`dd if=/sdcard/1.img of=/dev/block/mmcblk0p1,dd if=/sdcard/2.img of=/dev/block/mmcblk0p2`等等等等............................
    
    当然，像 system 分区， vendor 分区，userdata 分区，super 分区，这些分区就没必要进行备份还原了。
    
    查看分区信息的命令：
    
    先安装busybox的面具模块：链接: `pan.baidu.com/s/1hFQr0nvXprzcz2gyQxtFzQ` 提取码: `y61r`
    
    然后终端命令：`busybox fdisk /dev/block/sda` 回车，然后再输入p回车，就可以看到sda这块硬盘的所有分区信息了。adb,adc,add,ade,adf
    
    同理,emmc闪存手机的命令是：busybox fdisk /dev/block/mmcblk0回车，再输入p回车，就能看到所有分区信息了。
    

如果你的手机已经出现问题，且没有备份完整字库……去售后换主板，或者找个同机型的，用他的完整备份字库刷入，当然我并不确定是否成功，因为会不会黑砖，这是个待验证的问题。

而且最好别全部使用别人的手机的全字库备份，就算不黑砖，也会大概率出现 bootlocker 永久锁定，永久无法再次解锁，只能换主板。








[^1]:**所需资料打包**<https://push.dianas.cyou/LIS/Share/Root/>
[^3]:[Android 玩家必备神器入门：从零开始安装 Magisk - 少数派 (sspai.com)](https://sspai.com/post/67932)
[^15]: 告诉大家如何防止掉基带问题 [https://www.coolapk.com/feed/21305538](https://www.coolapk.com/feed/21305538)
[^17]:常识基础 [https://mi.fiime.cn/tutorial](https://mi.fiime.cn/tutorial)