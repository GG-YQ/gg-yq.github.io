- [软件工具](../software.md#常用方案)

# 系统
## Linux
- 运行界面
    - 命令行界面：命令行界面（CLI）在操作系统内核启动后直接进入，用的是字符模式，通过键盘输入命令和参数，然后在屏幕上显示文本输出。
    - GUI界面
        - 显示管理器(登录管理器)：登陆认证、启动显示服务器和窗口管理器、加载桌面环境。没有显示管理器则只能通过命令行登陆认证并进行后续启动操作。
        - 显示服务器：显示服务器负责管理其客户端和硬件设备之间的通信，如键盘和鼠标事件。图形应用程序通过显示服务器访问屏幕像素和进行屏幕绘图。图形显示协议：
            - X11协议：xorg
            - Wayland协议
        - 窗口管理器：管理多个GUI程序，各个窗口布局、开关、放缩...
        - 桌面环境：包括多个组件，任务栏、状态栏、桌面、终端模拟器...
- 系统目录
    ```markmap
    - /
        - bin: 最经常使用的命令(二进制文件Binaries)
        - boot: 启动 Linux 时使用的一些核心文件，包括一些连接文件以及镜像文件
        - dev: Linux 的外部设备(Device)
        - etc: 所有系统管理所需要的配置文件和子目录(Etcetera)
        - home: 用户主目录
        - root: 系统管理员目录，也称作超级权限者的用户主目录
        - lib: 系统最基本的动态连接共享库，其作用类似于 Windows 里的 DLL 文件。几乎所有的应用程序都需要用到这些共享库。
        - media: 挂载 linux 系统自动识别的U盘、光驱等
        - mnt: 挂载用户临时的文件系统(光驱等)
        - opt: optional(可选)是给主机额外安装软件的目录
        - proc: Processes(进程)是一种伪文件系统（也即虚拟文件系统），存储的是当前内核运行状态的一系列特殊文件，它是系统内存的映射，我们可以通过直接访问修改这个目录里的文件来操作系统。
        - usr: unix system resources(unix系统资源)存放很多应用程序和文件，类似于 windows 下的 program files 目录。
        - var: variable(变量)目录中存放着在不断扩充着的东西，我们习惯将那些经常被修改的目录放在这个目录下。包括各种日志文件。
        - sbin: 存放系统管理员使用的系统管理程序
        - srv: 存放服务service启动后需要提取的数据，如网络服务所需的配置、资源、代码等。
        - ...
    ```

- [环境变量设置](https://www.cnblogs.com/renyz/p/11351934.html)
    - 查看
        - `env`列出所有环境变量值
        - `echo $PATH`查询当前环境变量中的`PATH`变量
    - 设置
        - 当前shell临时变量: `export [-fnp] [变量名称]=[变量设置值]`
        - 持久变量: 把export命令添加到配置文件，如`~/.bashrc`
    - 设置文件启用顺序：配置一般写在`~/.bashrc`中，`~/.profile`会读取`~/.bashrc`，这样可以保证login shell和交互式non-login shell得到相同的配置。
        |bash类型|交互式|非交互式|
        |-|-|-|
        |non-login shell(取得bash不需要重复登陆)|启动后读取`~/.bashrc`资源文件|继承上一个shell(父shell或当前shell)的全部环境变量：不会读取`~/.bashrc`，而是查找环境变量`BASH_ENV`，读取并执行`BASH_ENV`指向的文件中的命令。|
        |login shell(取得bash需要完整的登陆流程)|启动登陆后读取`/etc/profile`和`~/.profile`，退出时读取并执行`~/.bash_logout`|继承上一个shell(父shell或当前shell)的全部环境变量|
    - 设置的文件目录
        |目录|作用范围|场景|
        |-|-|-|
        |`~/.bashrc`(推荐)|特定用户；每次shell script执行均使用|设定本用户环境变量，路径、函数、命令别名...|
        |`~/.profile`|特定用户；登入时使用一次|设定本用户环境变量，会调用`~/.bashrc`|
        |`/etc/bash.bashrc`|所有用户|系统bash环境|
        |`/etc/profile`(不推荐修改)|所有用户|系统环境变量，会调用`/etc/profile.d/`|
        |`/etc/profile.d/`(推荐)|所有用户|系统环境变量：直接修改`/etc/profile.d/`下对应的`.sh`脚本即可，例如`ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh`，然后`source /etc/profile`生效|

- 执行脚本：命令执行需在filename所在目录下，否则需要绝对路径或环境变量包含filename。
    - `source filename`、`. filename`: 当前shell进程执行，结束后返回当前shell进程。sh不支持source，bash支持source。
    - `sh filename`、`./filename`: 在子shell进程执行，结束后返回当前shell进程。，需要确保文件`./filename`具有可执行权限，`chmod +x ./filename.sh`。
    - `exec commandxxx`: 当前shell进程执行，结束后退出当前shell进程。exec命令可以提高系统的性能，因为它减少了创建新进程的开销。exec命令还可以用来修改当前shell的环境变量，文件描述符，信号处理等设置。

- bash脚本: 历史bash指令查看`cat ~/.bash_history`、`history 5`；脚本查看`view xxx.sh`；脚本编辑`vim xxx.sh`
    |命令|说明|
    |-|-|
    |`#!/bin/bash`|首行指定解释器为`/bin/bash`|
    |`$vname`;`${vname}`|变量名前加上$来使用变量，可以使用{}明确变量的边界|
    |`mkdir -p new_dir1/new_dir1_1`|创建嵌套目录|
    |`bash Miniconda3.sh -b -u -p ~/miniconda3`|-b批处理不需要用户交互；-u发现已有安装则更新安装；-p ~/miniconda3指定安装目录|
    |`cd ~`|切换到当前登录用户的主目录，如`cd /home/uname`|
    |`echo "xxxx"  >> xxx.xx`|追加写入：`>`覆盖；`>>`追加|
    |`touch xxx.xx`|创建空文件`xxx.xx`，如果⽂件已存在会修改⽂件时间戳|
    |`cat -n xxx.xx`|读文件`xxx.xx`附带行号|
    |`\|`|管道: 上一条命令的输出，作为下一条命令的输入参数|
    |`\|\|`|表示上一条命令执行失败后，才执行下一条命令|
    |`>`;`&>`|输出重定向：将正常信息重定向; 输出重定向：将错误信息或者普通信息都重定向输出|
    |`<`;`&<`|输入重定向; 输入文件合并|

- 扩容：扩容后修改`/etc/fstab`配置自动挂载
    - 分区设置
        - 一般分区设置
        - LVM分区设置：物理卷PV(硬盘或硬盘分区)$\rarr$卷组VG$\rarr$逻辑卷LV
    - 目录扩容：–o umask=000 控制分区读写权限
        - 分区挂载到目录
        - 目录挂载到目录
        - 目录软链接到目录
    - Q/A
        - ntfs挂载权限问题：ntfs格式的分区中并没有为文件预留属主等属性的地方，无法修改分区的属主、读写权限。
        - /mnt/xxx：默认所有者为root，读写可能有权限问题
        - /media/username/xxx：默认为所有者为username

- apt和apt-get
    - apt是apt-get和apt-cache命令的子集：更适合日常使用，因为它提供了更友好的用户体验和必要的命令选项。
    - apt-get则更适合用于编写脚本和实现自动化管理，因为它的输出格式更稳定。
    
## Win
- 装机
    - U盘启动盘：Ventory作为引导可把系统镜像、其它PE镜像直接放到U盘里使用。
        - 系统镜像iso文件
        - 其他PE系统转iso镜像再放到U盘
    - NUC M15装机
        - 制作系统安装引导盘
        - DG格式化系统盘
        - 从U盘启动安装程序(不拔)完成系统安装
        - 安装驱动：安装NUC M15官方驱动，新win11版也适合win10系统，旧win11+10版camera驱动有问题；系统更新；Nvida官网显卡驱动；尽量避免第三方补充的驱动。
- cmd命令行
    - 查看盘符
        1. 进入diskpart：```diskpart```
        2. 查看分区：```list vol```；
        3. 查看磁盘：```list disk```、```select disk 0```、```detail disk```；
    - 切换目录
        - 切换盘符：```D:```
        - 切换文件目录：同一盘符下：`cd C:\gyq\topush`；不同盘符下：`cd /d C:\gyq\topush`
- 程序搜索顺序
    - cmd命令中带路径，只在该路径中寻找文件，而不会到环境变量中去找。如果文件名不带后缀，则跟第一种情况一样，在指定目录中寻找这个名称的可执行文件或批处理文件执行，找不到报错；如果带后缀，若存在，则执行或用默认程序打开，若不存在，寻找该文件名+可执行文件或批处理文件后缀的文件来执行，找不到报错。
    - 输入的命令不带后缀（不带路径）
        1. 先会在无后缀的系统命令（如cd、dir等）中搜索，如果找到了就执行该命令
        2. 如果在无后缀的系统命令中找不到，则在当前目录中查找该命令+.exe、.msc、.bat等后缀的可执行文件或批处理文件，如果找到了则执行
        3. 如果没找到，最后再在环境变量那些目录中按上述规则搜索
     - 输入的命令带后缀（不带路径）
        1. 首先在当前目录中搜索该文件，若存在，如果该文件是一个可执行文件或批处理文件，则执行之，如果是其他一般文件则用与该类型文件关联的默认程序打开它； 
        2. 若当前目录不存在该文件,则在当前目录中查找是否存在以该文件名+可执行文件或批处理文件后缀（.exe、.bat、.msc等）命名的文件，如果找到了则执行之;
        3. 如果在当前目录中上述两种情况都未找到，才在环境变量所设置的那些目录中按上述顺序搜寻。先是按cmd命令所给的准确文件名查找，如果有，是程序或批处理则执行，是其它文件就用默认程序打开;
        4. 如果在环境变量目录中未找到该文件，再在环境变量目录中查找是否存在该文件名+可执行文件或批处理文件后缀（.exe、.bat、.msc等）的文件，如果找到了则执行之;
        5. 如果还是没有，则报错.

## shell脚本
- 路径
    |路径|`/`|`./`|`../`|
    |-|-|-|-|
    |说明|根目录|相对当前同目录下|相对当前向上1级，`../../`向上2级|
    |shell||`xxx`和`./xxx`不同：`xxx`在linux 系统会去 PATH 里寻找||
    |vscode|打开文件为默认根目录|`xxx`和`./xxx`等同||
    |.md||`[文件链接](./)`: vscode里有效，docsify里所有链接处理均从根目录开始拼接，因此要使用绝对路径或设置相对目录。<br>`![图片链接](./)`: 在vscode和docsify均有效。||
    |.py .ipynb|根目录默认同vscode|||

- 注意
    - 变量赋值符号`=`前后不能有空格
    - `[`、`]`、比较符号...前后必须有空格 

# 软件安装
- PC: ubuntu, * snap, ** 官网;
    |类型|Win|Linux|
    |-|-|-|
    |浏览器：Edge|&check;|&check;**|
    |社交：微信、QQ、腾讯会议|&check;|&check;**|
    |Office：WPS|&check;|&check;**|
    |Office：其他|MSOffice|LibreOffice|
    |资料管理：百度云|&check;|&check;**|
    |资料管理：[zotero](https://zhuanlan.zhihu.com/p/689468632)|&check;|&check;*|
    |资料管理：[docsify+github+giscus](gg-yq.github.io)|||
    |code：git;vscode*;node.js;miniconda;docker;|&check;|&check;|
    |3d建模：blender|&check;|&check;*|
    |OCR工具|ShareX|PaddleOCR部署;Tesseract部署;|
    |ASR工具||Whisper部署|
    |下载工具|迅雷|aMule*;Tranmission;|
    |翻译工具|有道;goldendict|goldendict|
    |更多工具|需安装:7-ZIP、鲁大师、剪映; Ditto共享粘贴板 <br>免装: 硬件管理(图吧工具箱、CrystalDiskInfo、3DMark); ffmpeg、v2rayN(科学上网winXray、v2rayN、Clash、Qv2ray); PDF Password Remover；|vim;ffmpeg;v2rayN;7-ZIP;[scrcpy](https://github.com/Genymobile/scrcpy)|

- Mobile
    淘宝、支付宝、UC、高德地图、咸鱼、拼多多、京东、多点、美团、滴滴、58；  
    微信、QQ、腾讯会议、订阅号助手；  
    百度网盘、网易公开课、网易云音乐；  
    bilibili、抖音、小红书、微博；  
    中国建设银行、中国农业银行、新网银行、买单吧、个人所得税；  
    知乎、萝卜投研、雪球股票、中信证券交易app、涨乐财富通、涨乐期赢通；  
    chinadaily、多次元托福、流利说；  
    其他：中国电信、WIFI万能钥匙、wps office、华为运动健康

- anki: https://apps.ankiweb.net/
    - https://blog.wedaily.cn/archives/ubuntuan-zhuang-ankiji-da-jian-zi-tuo-guan-tong-bu-fu-wu

- 研究
    - researcher-app

- 游戏
    - Epic、steam、steamVR、VD
    - 87VR助手

- 抓包
    - Wireshark
    - Browser DevTools
    - PacketTotal

- 远程控制
    - pc、手机：SunloginClient

- 视频和直播：OBS、Kdenlive、Shotcut、DaVinci Resolve

- adobe替代
    Photoshop——替代品——GIMP
    After Effects——替代品——Natron
    Premiere——替代品——Olive、OpenShot
    Illustrator——替代品——Inkscape
    Lightroom——替代品——digiKam

- 绘图：Krita

# Docker
## 容器使用
- 基础概念
    - 镜像：本地存储目录为/var/lib/docker/image/overlay2
    - 容器：Docker Daemon创建容器时在镜像层(rootfs)之上挂载一层读写层(read-write filesystem)，这一层文件系统称为容器层。
        - 容器读写层：存储对容器的修改，容器重启后不会丢失，容器被删除后会丢失。IO性能低、容量受限。
    - 挂载目录：属于宿主机文件，容器删除不会丢失。

- docker容器图形化界面显示方案: linux目前的主流图像界面服务X11支持客户端/服务端（Client/Server）的工作模式。docker作为客户端输出GUI应用信号，显示端作为服务端渲染。
    - 宿主机显示：`apt-get install x11-xserver-utils` ,`xhost +`
    - 远程显示：ssh
    - [参考docker-wine](https://hub.docker.com/r/scottyhardy/docker-wine) [tobix/wine](https://hub.docker.com/r/tobix/wine)

- 常用命令
    ```
    //服务操作(sudo): docker.socket会监听并适时自动重启docker服务，需要先停止docker.socket服务，然后停止docker.service服务。
    #查看Docker服务状态
    sudo systemctl status docker
    #关闭docker.socket服务
    systemctl stop docker.socket
    #关闭docker.service服务
    systemctl stop docker.service
    #start/stop/restart/disable(开启/关停/重启/禁用开机自启)
    systemctl restart docker
    #守护进程重启: 重新加载所有单元⽂件，配置变更生效，不会直接影响运⾏中的服务，需要⼿动重启服务以应⽤。
    systemctl daemon-reload

    //镜像操作: 1.本地镜像 2.拉取一个ubuntu镜像 3.搜索httpd镜像 4.删除hello-world镜像 5.初次创建并开启容器 6.ubuntu镜像层历史
    docker images
    docker pull ubuntu:13.10
    docker search httpd
    docker rmi hello-world
    docker history ubuntu

    //创建容器：docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
    docker run -i -t -d --name=paddleocr -v /hostdir:/dockerdir name_images:tag /bin/bash 
    --name=""指定容器名字
    -it终端交互模式
    -d后台模式
    -v挂载
    -p端口映射
    --entrypoint command: 用command覆盖dockerfile设置的默认entrypoint
    --restart: 容器的重启策略，no、on-failure、always、unless-stopped
    --privileged开启用户超级权限，配合-v /dev/bus/usb:/dev/bus/usb访问宿主机usb设备https://docs.pingcode.com/baike/3472113
    --device: 添加设备，容器可能需要安装驱动等系统依赖才能使用设备。--device=/dev/video0添加摄像头，--device=/dev/snd添加声卡，--device=/dev/ttyUSB0添加USB设备。

    //容器操作：ps/rm/start/stop/restart(查看/删除/启动/停止/重启)
    docker restart my_container
    docker attach <Name of container>
    docker logs container_name
    docker exec container_name ls

    //调试
    #在运行的容器中执行命令exec: 例如打开一个终端
    docker exec -it 容器名 /bin/bash
    #容器内文件copy到本地
    docker cp 容器名:文件完整路径 本地路径
    #本地文件copy到容器内
    docker cp 本地文件 容器名:文件完整路径

    docker history imageID
    docker inspect containerID
    docker stats
    docker logs CONTAINER

    #查看网络、卷
    docker network ls
    docker volume ls

    //清理
    docker system prune -a
    docker volume prune
    ```

## Dockerfile
- alpine/dfimage分析镜像dockerfile工具
- 基本原则
    1. 无状态原则
        - 状态设置在挂载卷等镜像外部
        - `FROM`基础镜像指定确定的版本，默认的`latest`可能会随仓库更新改变
    2. 精简原则
        - `&& \`合并`RUN`指令减少镜像层
        - `COPY`结合`.dockerignore`过滤容器不需要的或敏感的文件
        - 清理不需要的安装文件和缓存: `apt-get clean`只会清理`/var/cache/apt/archives`目录中除锁定文件之外的所有内容。
            ```
            rm -rf /var/cache/apt 或者 rm -rf /var/cache/yum
            rm -rf /var/cache/apt-get && \
            apt-get clean && \
            conda clean -a && \
            rm -rf /app/
            ```
        - 通过多阶段构建可以过滤编译阶段的环境和文件

- 基本语法
    1. ARG定义的构建参数只在构建过程中有效，不会被包含在最终的镜像中。ARG如果在FROM指令之前指定，那么只能用于FROM指令中。要想在FROM之后使用，必须再次声明(不用再次赋值)。
    2. ENV定义的环境变量参数会在最终的镜像中持久化。
    3. WORKDIR指令可以指定后续各层构建命令的镜像内目录和容器运行时的工作目录，如该目录不存在会自动创建。
    4. EXPOSE指令声明容器运行时提供服务的端口，这只是一个声明，在容器运行时并不会因为这个声明应用就会开启这个端口的服务。在 Dockerfile 中写入这样的声明有两个好处，一个是帮助镜像使用者理解这个镜像服务的守护端口，以方便配置映射；另一个用处则是在运行时使用随机端口映射。
    5. RUN、COPY、ADD镜像构建时执行。
        - `RUN cp x /y/y`之前最好`mkdir -p /y/y`，直接cp可能报错。
        - RUN避免交互式的命令：`apt-get install -q -y --no-install-recommends`
    6. ENTRYPOINT、CMD容器开启时执行。可以设置一些启动前的准备工作。
    ```
    FROM ubuntu:24.04
    LABEL maintainer="gg"
    RUN apt-get update && \
        apt-get install -y python3 python3-pip && \
        apt-get clean
    WORKDIR /app
    COPY . /app
    RUN pip3 install -r requirments.txt
    CMD ["python3","--version"]
    ```
- `SHELL ["/bin/bash", "-c"]` #指定shell为bash: 默认的sh支持`.`，不支持`source`。ENTRYPOINT["source /etc/profile"]报错？
- 构建命令：docker build --no-cache -f Dockerfile -t image_test:tag_1 .
    ```
    docker build [OPTIONS] PATH | URL | -
    常用选项
    -f, --file: 指定 Dockerfile 的路径，Dockerfile不必须在上下文路径中。
    --build-arg: 设置构建参数
    -t, --tag: 为构建的镜像指定名称和标签
    --no-cache: 不使用缓存层构建镜像
    PATH 指的是包含 Dockerfile 的目录路径，可以使用 . 来代表当前目录。镜像构建的上下文，"."指上下文为执行build命令的同目录。上下文路径下的所有文件会被打包上传到docker引擎，所以一般将Dockerfile文件放在空目录或者项目所在的根目录，可以用.dockerignore过滤以减小上传文件大小。COPY、ADD等命令均从该上下文路径下获取源文件。
    URL 指向包含 Dockerfile 的远程存储库地址，例如 Git 仓库
    - 表示从标准输入读取 Dockerfile
    ```

## 迁移
```
# 单个镜像迁移
docker save image-name > image-name.tar
docker load < image-name.tar
# 批量镜像迁移
docker images -q | xargs -I {} docker save {} > {}.tar
find . -name "*.tar" -exec docker load < {} \;

# 容器迁移
docker export container-name > container-name.tar
docker import container-name.tar image-name
```

# VSCode
- 基本使用——代码调试
    - 安装
        - OS内安装编译器/解释器
        - VSCode内安装相关插件：辅助编写和调试(例如Code Runner支持运行多种编程语言的代码)
    - 调试
        - F5/`Run`：在`.vscode > launch.json`文件里配置默认的解释器，调试`run`后在`OUTPUT`查看结果
        - 在内置终端运行：命令行指定解释器和程序文件路径，执行后在`TERMINAL`查看结果
    - 其他
        - tasks.json：定义开发流程，编码、构建、运行/调试、测试、打包
        - launch.json：定义运行调试

- 基本设置
    - 用户设置 (User Settings)
        - 属于全局设置
        - 设置通常位于用户目录下
    - 工作区设置 (Workspace Settings)
        - 仅适用于特定的工作区或项目，可以覆盖用户设置。
        - 设置存储在项目目录下的.vscode/settings.json

- 插件安装：推荐登陆账号使用Settings Sync功能同步设置、插件<a id="vsc"></a>
    |插件类型|插件名称|
    |-|-|
    |c++/c#|.NET Install Tool;|
    |python|python;jupyter|
    |web|open in browser; Live Server|
    |笔记|markdown all in one; markdown preview enhanced;[markmap](https://markmap.js.org/repl);[marp](https://marp.app/)|
    |AI|ChatGPT; copilot;|

- 常见问题
    - 代码目录下生成的".vscode"文件夹只对阅读代码有影响而对编译器无影响，并且这个文件夹产生的数据极大，远超出github仓库允许的容量(100M)，一般不push。
    - 安装包存在依然提示"import cannot resolved..."：python.analysis.extrapaths设置参考https://blog.csdn.net/weixin_43937790/article/details/128039587 https://learnscript.net/zh/python/development-tools/vscode/pylance/
    - 自动格式化需设置忽略排序：可能会产生import依赖问题
    - marp预览问题: MPE冲突
        - To use Marp preview while using MPE, open the command palette via Ctrl (Cmd) + Shift + P and choose "Markdown: Open Preview to the Side" for VS Code built-in preview, instead of "Markdown: Markdown Preview Enhanced: Open Preview to the Side".
        - To restore a VS Code original preview button from the toolbar, disable markdown-preview-enhanced.hideDefaultVSCodeMarkdownPreviewButtons the MPE extension setting.
    - marp在vscode中html支持选项：`Markdown > Marp: Enable HTML` from preference.
    - marp：图片引用'/'可预览但不能导出，需要改为'../../'

## python
- python环境设置
    1. conda新建环境
    2. 激活环境：linux下bash激活; windows下cmd(prompt)激活环境，powershell无法激活。
    3. vscode默认python解释器设置为指定环境下的解释器：ctrl+shift+p>Python: Select Interpreter>选择要使用的环境的python解释器。

- 解释器找不到？
    - 分别在venv Folders 和 venv Path中添加虚拟环境文件目录路径，重启VScode设置生效


## git
- vscode内github新旧库连接
    1. 前置：git全局设置以及github连接key设置
    2. 连接
       -  直接clone会自动建立连接：github新建repository,设置.ignore模板为python,设置license模板。
       - 或者git add设置远程连接并pull。

## devcontainer
- [使用说明](https://code.visualstudio.com/docs/devcontainers/containers)
    ![](./_res/architecture-containers.png)
    - 已有容器：直接attach正运行的容器
    - 新建容器
        - dockerfile：安装miniconda后释放空间`/opt/xxx/bin/conda clean -afy`；安装开发过程所需的依赖(OS-/lib的依赖、python-requirements.txt的依赖)
        - devcontainer.json：设置在`.devcontainer/devcontainer.json`或者`.devcontainer.json`
    
        ```devcontainer.json
        // For format details, see https://aka.ms/devcontainer.json. For config options, see the
        // README at: https://github.com/devcontainers/templates/tree/main/src/miniconda
        {
        "name": "ide_gg",
        "build": { 
            "context": ".", //Path that the Docker build should be run from relative to devcontainer.json. ".." 将引用相对`.devcontainer.json`上一级目录中的内容，默认为 同级"."。
            "dockerfile": "Dockerfile" //The path is relative to the devcontainer.json file.
        },
        "mounts": [
            {"source": "/mnt/mydisk1_ext4/data",
            "target": "/outdata",
            "type": "bind" }
        ],
        
        // 设置进入容器后的工作目录：默认是`/workspaces/你的目录名`(`workspaceMount`的默认参数会自动挂载`/workspaces/你的目录名`)，如果打开的项目很大容器启动和后续容器中的操作都会很慢，所以不直接在`workspaces/你的目录名`下进行开发，而是执行一个提前创建好的工作目录`/app`，可以写在 Dockerfile 中。
        "workspaceFolder": "/app",
        
        // 容器关闭后需要执行的操作，这里是停止容器
        "shutdownAction": "stopContainer",
        
        // 容器的权限，这里设置为 root
        "remoteUser": "root",
        
        // 一些自定义设置：插件...
        "customizations": {
            "vscode": {
                "extensions": [
                    "ms-python.python"
                ]
            }
        }
        }
        ```
    
- 使用原则
    - container：开发环境、和源代码有关的vsc插件。
    - 本地挂载：源代码
    - 本地vsc：自动默认配置编译结果输出文件夹、git credentials等等

- conda_envs: 安装在挂载位置
    ```
    # 创建
    conda create --prefix=/hostdata/envs/py3_7 python=3.7
    # 激活
    conda activate /hostdata/envs/py3_7
    ```

# git

![](./_res/image1.png)

- 基本用法
    - 用vs打开项目文件夹，进入项目目录：所有git命令都要在项目空间下进行，如果需要新建或进入其他目录则需要执行下面的代码
        ```
        $ pwd  //mac中查询当前目录，windows当前目录在命令头展示  
        $ mkdir git-tutorial  
        $ cd git-tutorial  
        ```  
    - 主分支设置为main: github把master默认分支改为了main，git要做相应调整，把本地git的master改成main。
        - 把默认分支改为main
        ```
        \\使用git init初始化项目时, 默认使用main做为主分支
        $ git config --global init.defaultBranch main
        \\或者在执行git init时指定初始分支名称
        $ git init -b main
        ```
        - 修改已创建并push过的项目的主分支为main
        ```
        \\把当前master分支改名为main；删除远程master分支，该分支为远程主分支时无法删除，只需在远程修改default branch为其他分支；推送本地分支到远程仓库。
        $ git branch -M master main  或直切换到主分支master，执行$ git branch -M main
        $ git push origin --delete master
        $ git push -u origin main
        ```  

    - 远程库的连接和解除：直接clone会自动创建连接
        ```
        //第一次通过git去使用GitHub需要全局设置：--global针对系统上所有仓库有效；-e针对当前仓库有效
        $ git config --global user.name "xxxx" 
        $ git config --global user.email "xxxx@xxx"
        $ git config --global --list //查看操作是否完成
        $ ssh-keygen -t rsa -C "xxxx@xxx" //邮箱和上述邮箱一致，一直回车可略过密码等设置，找到id_rsa.pub，复制内容，添加到github的ssh keys。提示"unknown key type -rsa"时，直接使用$ ssh-keygen -C"xxxx@xxx"
        $ ssh -T git@github.com //选择yes，验证是否成功
        //建立连接：Git支持多种协议(包括https)，但ssh协议速度最快
        $ git remote add origin git@github.com:username/reponame.git
        不推荐 $ git remote add origin https://github.com/username/reponame.git
        //远程库的查询和删除：先用git remote -v查看远程库信息；然后用git remote rm根据名字删除，比如删除origin，即解除远程关联。
        $ git remote -v  
        $ git remote rm name
        ```  
    - 提交到库：rm删除文件、add添加文件到暂存区；commit通过暂存区的指针将暂存区的快照提交到本地git库；push同步到远程库，第一次推送main分支时加上了-u参数，Git不但会把本地的main分支内容推送到远程新的main分支，还会把本地的main分支和远程的main分支关联起来，在以后的推送或者拉取时就可以简化命令。
        ```
        $ git rm <file>
        $ git add xxxx.xxx
        $ git commit -m "first commit or some note"
        $ git push -u origin main
        ```  
    - 远程库操作详解
        ```
        //clone：切换到目标文件目录，clone仓库到本地让自己能够查看修改，有无仓库权限均可，适用本地为空
        $ git clone git@github.com:username/reponame.git

        //pull：切换到目标文件目录，pull从远程获取代码并合并本地的版本，必须有仓库权限。pull相当于$ git fetch +$ git merge FETCH_HEAD的简写，命令格式为"$ git pull <远程主机名> <远程分支名>:<本地分支名>"，如果远程分支是与当前分支合并，则冒号后面的部分可以省略。
        $ git pull origin main
        //如果pull报错"refusing to merge unrelated histories"，原因是两个仓库不同而导致的，要添加参数--allow-unrelated-histories将两个项目合并。
        $ git pull origin main --allow-unrelated-histories

        //push：本地推送分支，格式为"$ git push <远程主机名> <本地分支名>:<远程分支名>"；如果本地分支名和远程分支名一样，可以省略":<远程分支名>"；如果远程主机中不存在该分支，那么会被创建；如果本地分支已经跟远程分支建立了追踪关系，那么可以省略"<远程主机名>"和":<远程分支名>"。push如果报错"Updates were rejected because the tip of your current branch is behind"，则需先通过pull更新本地版本再push。
        $ git push origin main

        //在本地创建和远程分支对应的分支：本地和远程分支的名称最好一致
        $ git checkout -b branch-name origin/branch-name
        //建立本地分支和远程分支的关联
        $ git branch --set-upstream branch-name origin/branch-name

        //git sparse checkout (稀疏检出)：切换到目标目录初始化init；建立连接；设置稀疏检出为true；echo指定要检出的部分；pull将指定的部分拉取到本地。后续push操作将只影响远程的该部分。
        $ git init <project> 
        $ git remote add origin https://*****.git
        $ git config core.sparsecheckout true
        $ echo "path1/" >> .git/info/sparse-checkout
        $ echo "path2/" >> .git/info/sparse-checkout
        $ git pull origin [branch]   //这里指定远程的分支
        ```  
    - git忽略文件设置：[模板参考](https://github.com/github/gitignore)；[忽略规则参考](https://www.cnblogs.com/kevingrace/p/5690241.html)
        ```
        1. 创建.gitignore文件
        在版本管理的根目录下（与.Git文件夹同级）创建一个 .gitignore，命令为：touch .gitignore
        2. 直接用vscode打开编辑，写入要忽略的文件或文件夹并保存
        .gitignore
        .vscode/
        **/__pycache__
        3. 强制添加一个被.gitignore忽略了的文件xxxx.xxx到Git
        $ git add -f xxxx.xxx
        4. 检查哪个规则忽略了文件xxxx.xxx
        $ git check-ignore -v xxxx.xxx
        5. 未生效原因排查：.gitignore只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。解决方法就是先把本地缓存删除（改变成未track状态），然后再提交
        git rm -r --cached .
        git add .
        git commit -m 'update .gitignore'
        ```  
- 分支管理
    - 分支查看
        ```
        //git branch命令会列出所有分支，当前分支前面会标一个*号
        $ git branch
        //git branch -vv命令，可以查看本地分支跟远程分支是否存在追踪关系
        $ git branch -vv
        ```  
    - 版本恢复
        ```$ git reset --hard <commit_id>```
    - 回退到上一个版本：
        ```$ git reset --hard HEAD^```
    - 回退到commit_id以xxxx开头的版本
        ```$ git reset --hard xxxx```
    - git log可以查看提交历史，以便确定要回退到的左侧版本，HEAD指向当前版本
        ```
        $ git log
        $ git log --pretty=oneline
        $ git log --graph --pretty=oneline --abbrev-commit
        ```
    - 用git reflog查看历史命令，以便确定右侧版本
        ```$ git reflog```
    - 创建并切换到分支bname
        ```
        $ git checkout -b <bname>  
        $ git switch -c <bname>
        ```
    - 创建新分支newbname
        ```$ git branch <newbname>```
    - 切换到分支bname
        ```
        $ git checkout <bname>
        $ git switch <bname>
        ```
    - 合并某分支到当前分支：通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
        ```
        $ git merge <name>
        $ git merge --no-ff -m "merge with no-ff" dev
        ```
    - 删除分支：如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除
        ```
        $ git branch -d <name>
        $ git branch -D <name>
        ```
    - bug分支：修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；当手头工作没有完成时，先把工作现场```$ git stash```一下，然后去修复bug，修复后，再```$ git stash pop```，回到工作现场；在master分支上修复的bug，想要合并到当前dev分支，可以用```$ git cherry-pick <commit>```命令，把bug提交的修改“复制”到当前分支，避免重复劳动。

- 标签：tag是一个有意义的名字，跟某个commit绑在一起
    - 新建一个标签：默认为HEAD，也可以指定一个commit id；-a指定标签名，-m指定说明文字
        ```
        $ git tag <tagname> <commit id>
        $ git tag -a <tagname> -m "blablabla..." <commit id>
        ```
    - 查看所有标签
        ```$ git tag```
    - 推送一个本地标签
        ```$ git push origin <tagname>```
    - 推送全部未推送过的本地标签
        ```$ git push origin --tags```
    - 删除一个本地标签
        ```$ git tag -d <tagname>```
    - 删除一个远程标签
        ```$ git push origin :refs/tags/<tagname>```

- 优化
    - 彻底删除commit和大文件提交：git branch-filter删除所有记录中的大文件并强制推送远程库
    - git rebase commit整理：旧提交依然存在于隐藏分支
    - 只保留最新的版本
        - 本地方案一：设置--depth==1然后克隆，从而实现本地只有最后一个版本的记录
        - 本地和远程方案二：创建并切换到lastest_branch分支git checkout --orphan latest_branch; 添加所有文件git add -A; 提交更改git commit -am "删除历史版本记录，初始化仓库"; 删除分支git branch -D main; 将当前分支重命名git branch -m main; 强制更新远程库git push -f origin main.

- FQ
    - 在git bash命令行git commit -m "messages"可以正常commit，但是使用vscode工具栏commit一直卡住：vs code升级后，原来提交代码时，是在vscode里直接填写message的，升级之后没有了，会直接对代码进行提交，这样的话导致服务器拒绝。
        ```
        解决办法：在设置里改回旧版本的提交方式。file>>preferences>>settings，取消勾选“use editer as commit input”。
        ```
    - 其他：diff在commit前查看区别；status查看工作目录和暂存区域状态
        ```
        $ git diff
        $ git status
        ``` 
# Node.js
[安装docsify-cli](https://cloud.tencent.com/developer/article/1943482?from_column=20421&from=20421)


# python工具
## 常用
- 管理工具
    ||环境管理|包管理|
    |-|-|-|
    |pip|&cross;|只支持Python依赖；在需要先切换到指定环境中再使用pip命令；pip不将python视为包无法更新python；pip可以安装一些conda无法安装的包。|
    |conda|&check;|支持Python以外的依赖，如CUDA；可跨环境安装包；可以安装一些pip无法安装的包。|
    |uv|&check;|pip+virtualenv+pip-tools的整合|

- 路径
    - 解释器路径
        ```
        which python3 #当前环境解释器路径
        ```
    - 导入模块搜索路径
        ```
        # 查看
        import sys
        print(sys.path)
        # linux设置
        echo "export PYTHONPATH=$PYTHONPATH:/path/to/your/utils" >> ~/.bashrc
        ```

- 常用库
    |功能|库|
    |-|-|
    |pdf处理|pdf2docx|
    |markdwon处理|mistune|
    |生成requirements.txt|pipreqs|
    |生成UML类图和包依赖关系图|graphviz+pyreverse|
    |生成函数调用图|graphviz+pycallgraph|
    |Turn your data scripts into shareable web apps|streamlit|
    |测试库|pytest|
    
## pip
- 本地安装：下载.whl到本地然后安装`pip install xxx.whl`，适合大文件情形
- 在线安装
    - 默认源直接安装`pip install xxx=0.0`；
    - 临时指定源安装`pip install -i https://pypi.tuna.tsinghua.edu.cn/simple xxx=0.0`；
    - 永久配置源`pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple`

## conda
- 基本工具
    - anaconda: python解释器+conda包管理器+常用的科学计算包
    - miniconda: python解释器+conda包管理器
        
- 基本命令
    ```
    conda init #初始化 Conda，使其在不同的 shell 环境中工作。
    conda -v
    conda search <模糊词>  #模糊查找包
    conda -h 
    
    更新
    conda update conda：更新conda，可能要以管理员身份运行。升级anaconda前需要先升级conda。
    conda update --all：更新所有包，包括anaconda发行版本身
    conda update anaconda：升级anaconda
    conda update spyder：升级spyder
    conda update <package_name>：升级指定的包

    包管理
    conda list  #显示当前环境中所有的安装包
    conda install <package name>  #当前环境中安装指定的包
    conda remove <package name>  #当前环境中删除指定的包
    conda install --name <env_name> <package_name>  #在指定环境中安装包

    环境管理
    conda env list：查看已经安装成功的所有环境
    conda create -n <envname> <python=3.10>：若没有指定python则只创建一个空conda环境。
    conda activate <env name>：进入环境
    conda deactivate：退出当前环境
    conda remove -n <env name> --all  #删除环境
    ```

- 环境迁移
    - 离线
        - 直接复制envs目录下的虚拟环境文件夹进行迁移，需要在目标电脑上配置环境路径。
        - 使用conda-pack工具迁移。
    - 在线：.yml和.txt结合进行迁移。从原环境导出.yml和requirements.txt，在新环境中依次安装conda环境和pip要求。使用conda环境文件管理项目的大部分依赖，使用pip安装某些不包含在conda索引中的包。
        - 使用conda环境文件environment.yml进行迁移：适用于跨平台和操作系统共享项目环境，需要联网。移植过来的环境只是安装了原环境里用conda install命令直接安装的包，用pip装的东西没有移植过来，需要重新安装。
        - 使用pip要求文件requirements.txt进行迁移：不推荐，因为只会导出使用pip安装的依赖包，不适用于虚拟环境的迁移。

# Zotero
- zotero迁移
    - 原数据存储文件Zotero直接复制到新存储位置
    - 修改默认存储位置后读写权限问题
- 官方文档 （https://www.zotero.org/support/）
- 官方论坛 （https://forums.zotero.org/discussions）
- Zotero Tips & Tricks （https://www.zotero.org/support/tips_and_tricks）
- 高手分享 （https://www.yangzhiping.com/tech/zotero1.html）
- [基础](https://pkmer.cn/Pkmer-Docs/11-zotero/zotero%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8/zotero%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8/)
    - 设置存储路径：在首选项中设置数据存储位置，存储路径下的zotero.sqlite 文件存储的是文献条目的信息，笔记以及标签；\storage 目录下存放的是文献的附件，对应生成一个以 8 个字符命名的子文件夹。
    - 关闭自动检索元数据：避免pdf导入卡顿
    - 设置引用样式
    - 设置第三方云平台同步：坚果云、微软的 OneDrive。
    - 设置插件：注意版本兼容
        > Sci-Hub Plugin for Zotero：下载文献；  
        Jasminum：兼容中文文献，在安装 Jasminum 插件时，如果想为知网下载的文献添加书签，还需要下载软件 PDFtk，同时在 首选项 中配置 PDFtk 的安装路径；  
        Zotero PDF Translate：翻译文献；  
        Zotero Better Notes：记笔记，Better Notes 提供了一些笔记模板，可以在这里下载。请注意，在命名模板时需要在名称前方加上关键词 [Item]。

- 导入条目：建议先根据DOI等信息创建条目，然后将pdf等资源添加到条目附件；不建议直接根据PDF文件识别文献元数据，可能识别失败或混乱。如果直接保存PDF至Zotero，Zotero会自动为其抓取相关书目信息并创建条目。但如果Zotero无法成功抓取到PDF的相关信息，则不会创建条目，使得该PDF成为一个独立附件。因此可以通过其他方式为独立附件创建条目（如通过网页保存、通过识别符等方式），或者直接将其拖拽到某个条目中。
    > 1. 在浏览器中点击右上角 Zotero 插件导入；
    > 2. 复制文献的 DOI 到 Zotero 中的通过标识符添加条目 。
    > 3. 这样导入的文献条目可能没有相应的 PDF 附件，这时候有两种办法：
    >> 下载好对应的 PDF 文件，右键条目 > 添加附件；  
    >> 下载 Sci-Hub 插件，通过插件下载 PDF 文件并添加到附件当中。

- 条目更新
    - 从分类移除条目：从分类中移除条目不影响其他分类，条目不会进入回收站，不会被删除。如果一个条目不属于任何分类，将在未分类条目一栏显示。
    - 删除条目(delete)：删除条目，然后在回收站一栏彻底删除。如果附件是以链接形式存储，彻底删除条目的同时不会从磁盘删除附件。

- 添加附件
    - 副本附件(直接拖拽或从网页保存快照)：副本附件是Zotero处理附件的默认方式，Zotero会自动复制文件，并将文件副本存进Zotero数据文件夹中作为附件进行管理。
    - 链接附件(拖拽时按住 Ctrl+Shift (Windows/Linux) 或 Cmd+Option (Mac))：链接附件指的是Zotero只保存附件在本地上的路径，而不是将附件复制进Zotero的数据文件夹中。由于链接附件使用的是本地路径，而本地路径并不能保证协作时其他成员能够成功访问附件，因此链接附件不支持Zotero的协作功能。如果您选择使用以链接形式保存附件，第三方插件ZotFile可以帮助您实现更高效的工作流。

- 一些问题
    |操作|问题|备注|
    |-|-|-|
    |批量导入|使用浏览器插件批量导入文献出现错误提示：保存此条目时出错。|尝试逐条导入|

# WPS
1. 显示格式TEXT()函数
=text(A1,”h小时mm分”)
=text(A1,”yyyy年mm月dd日”)
=text(A1,”aaaa”) #长星期格式”aaaa”，短星期格式”aaa”
=text(A1,”000”) #填入多位数序列
2. 日期格式yyyy-mm-dd转yyyy/m/d
- 使用text()
- 选中，分列-默认分隔符号选择tab-列数据类型选择日期-完成
3. 条件格式
选定区域-条件格式-公式-录入公式-格式设置
4. 显示分位和单位
自定义格式：0!.0,
5. 条件匹配
- 条件匹配单值、多值、最大值、最小值
- 单条件匹配单值：index+match
- 多条件匹配单值：将多条件通过&转化为单条件，然后使用index+match
- 单条件匹配多值：idnex+small+if
- 多条件匹配数字：averageifs()、sumifs()、sumproduct()
6. 维度转换
- 一维转二维：法一，透视表；法二，全量行标签进行条件匹配。
- 二维转一维：透视表
7. 切片器
8. 数组操作
- 公式法：适合少量计算，公式完成后需要同时Alt+Enter或Ctrl+Shift+Enter
    ```
    例如：根据B、A列条件，合并C列文本
    {=TEXTJOIN("；",1,IF(($B$2:$B$27=F$1)*($A$2:$A$27=$E2),$C$2:$C$27,""))}
    ```
- 透视表：自定义函数、Power Pivot


# SQL
1. Hive SQL
- Null：sum、count会忽略null、count(1)不会，或者嵌套nvl
- Union all
- 堆叠变二维：自身join求笛卡尔积，然后where或on过滤
- 窗口函数：sum()over()、row_number()over()
- 日期处理date_format()、date_add()、date_sub()、last_day()
- 时间戳和其他格式转换
- 多类聚合：grouping sets、rollup
- 空值：判断is null、=’\\N’；和’’空字符串不一样，空字符串需要用=’’判断；和’ ’空格也不一样；处理，nvl、nullif、coalesce()
- 随机选择num个：row_number()over(order by rand()) as rn where rn<=num
- 拆分：split、explode
- 字符串处理：concat()、concat_ws()、substr()、trim、rtrim、ltrim、Lpad()、Rpad()
- 格式转换：cast()
- 日期提取小时2位字符：.z_hour
2. Nosql
- 图表示

# SAS
数据导入：Excel只能用proc，不能用data步导入。
```
PROC IMPORT
DATAFILE="filename" | DATATABLE="tablename" (Not used for Microsoft Excel files)
<DBMS=data-source-identifier>
<OUT=libref.SAS data-set-name> <SAS data-set-option(s)>
<REPLACE;>
<file-format-specific-statements>;
```
- 必选参数只有一个，即DATAFILE|DATATABLE，其中DATAFILE可以用别名file代替，DATATABLE可以用别名table代替。
- DBMS=data-source-identifier：导入的数据的类型
- SAS data-set-option(s)： SAS data set的选项，比如可以使用where data set option.
- OUT=<libref.>SAS data-set：数据集的名子
- REPLACE：如果数据集已经存在，是否替换。
- file-format-specific-statements：文件格式说明，比如，对于Excel文档，GETNAMES=YES | NO可以规定是否使用文档中的第一行来产生SAS 变量，SHEET=sheet-name来指定文档中sheet的名子，每个语句是以逗号作为分割符。

# pandoc：docx2md
1. 先进入文档所在路径：转的文档需要和pandoc.exe在同一层级，否则路径错误执行是不会成功的。
2. 执行命令
    ```
    //在当前目录创建.md和media文件夹
    pandoc -f docx -t markdown --extract-media ./ -o aaa.md aaa.docx
    //在当前目录创建.md，在当前目录创建xxx/media文件夹
    pandoc -f docx -t markdown --extract-media ./xxx -o aaa.md aaa.docx
    ```

# 虚拟化
- 虚拟化对象
    - 计算资源：cpu
    - 网络资源：网络链路资源
    - 存储资源：内存、硬盘
    - 外设
        - 输入设备：键盘、鼠标、摄像头、麦克风、触控板、陀螺仪、其他传感器...
        - 输出设备:显示器、音响、打印机...

- 摄像头虚拟化：可以自定义视频源、访问不同摄像头流
    - OBS Studio：开源实时视频录制和直播软件，内置虚拟摄像头
        - 视频会议：https://www.obsproject.com.cn/obs/118.html
        - https://www.cnblogs.com/WuKaiXiong/p/OBS.html
        - https://zhuanlan.zhihu.com/p/594458635
        - https://www.bjdsby.com/h-nd-3859.html
        

- PC+移动摄像头
    - OBS+ninja &check;: 无需插件和移动端app
        - https://www.cnblogs.com/JiangOil/p/18299489
        - https://www.ufans.top/index.php/archives/963/
        - https://www.bilibili.com/video/av991514135/?vd_source=2a823ce6073f9ac24d39aaa3c97831d4
    - OBS安装Droidcam插件+移动端Droidcam应用
    - IP摄像头服务器+ADB端口转发或USB共享摄像头
    - 其他
        - https://www.obsproject.com.cn/other/162.html