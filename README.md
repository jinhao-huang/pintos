# Pintos

本仓库提供Pintos项目的初始代码。并提供Docker镜像来运行Pintos。

[Pintos](https://web.stanford.edu/class/cs140/projects/pintos/pintos.html)是一个基于x86架构的操作系统，以简单的方式支持了内核线程、加载、运行用户程序和文件系统。Pintos由Stanford开发，用于CS140课程的教学。同时也被Berkeley， JHU等学校的操作系统课程采用。~~也被我北工大采用。~~

Docker镜像已在Mac(Apple Silicon)和Windows平台上测试正常运行。如有其他问题欢迎提出issue。

## 如何运行

- 首先你需要在你的电脑上下载安装好[Docker](https://www.docker.com)和[Git](https://git-scm.com)。

> Windows用户可能需要安装WSL之后才能正确安装Docker

- 打开终端（对于Windows用户推荐使用PowerShell），输入命令`docker pull onebitbool/pintos`来拉取docker镜像。镜像压缩大小为1GB左右，你可能需要等待一定时间。期间保证网络稳定，丢失网络连接可能需要重新拉取。

> 如果你是北工大的学生，如果校园网拉取经常失败，可以考虑利用宿舍的校园网（不是bjut_wifi啊，每个寝室一个的那个）来拉取镜像。

- 拉取成功后，你需要获取Pintos代码到你的电脑上。在终端中使用`cd`命令进入你希望代码存放的路径，使用命令`git clone https://github.com/onebitbool/pintos.git`来拉取Pintos初始代码。

> 如果你不知道`cd`指令，你可能需要学习基本的Linux命令。我们运行在Docker上的环境**没有图形界面**。你需要适应命令行界面。如果你需要图形界面，你可以使用虚拟机来搭建运行环境。**但这会带来额外的性能损耗**。

> 本项目的代码在Pintos原始代码的基础做了一些适配。你可以在[这个链接](https://pintos-os.org/cgi-bin/gitweb.cgi?p=pintos-anon;a=summary)获取Pintos的原始代码，但你可能需要按照[官方指引](https://web.stanford.edu/class/cs140/projects/pintos/pintos_12.html)手动配置运行环境。

- 在终端使用命令`docker run -it --rm --name pintos --mount type=bind,source=<pintos代码绝对路径>,target=/home/pintos onebitbool/pintos bash`来在打开Pintos容器。

> **务必将`<pintos代码绝对路径>`替换为你拉取的初始代码路径**，你可以使用`pwd`命令来获得当前路径。

至此，你已经配置好了Pintos运行环境，任何时候你都可以在终端使用上面的命令来打开一个一次性的Pintos容器来运行你的代码。

## 验证运行环境

在容器环境下你可以使用下列命令来运行测试。

```shell
cd /home/pintos/src/threads/
make
cd build
make check
```

`make check`可能需要一些时间来运行，取决于你的机器配置，典型值应该在1分钟左右。

运行结束后，你应该可以看到这样的输出结果。

```
20 of 27 tests failed.
../../tests/Make.tests:26: recipe for target 'check' failed
make: *** [check] Error 1
```

最后，运行两次`exit`命令来退出容器环境。