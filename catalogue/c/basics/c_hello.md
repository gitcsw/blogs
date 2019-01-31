# 教程惯例:Hello World!

第一个程序，Hello World程序：
```c
#include <stdio.h>//引用头文件
int main(void)//入口函数
{
	printf("hello world\n");
    return 0;
}
```

### 0x01 不同平台的IDE以及编译器
---
linux下可使用gcc编译器：
vi/vim编辑器，输入此程序，保存文件为hello.c；
gcc hello.c -o hello  然后./hello 运行即可。

windows下可以IDE[集成开发环境(Integrated Development Environment)]进行可视化高效开发，如：Visual Studio 2017、Eclipse等。

### 0x02 编译第一个程序
---
这次以gcc编译为例：
- 文件保存不多说，上文已介绍；
- 安装Gcc:(网上有太多文章，没必要重写，直接借鉴修改如下)

Windows篇：(https://www.jianshu.com/p/dc0fc5d8c900 作者：飘荡的叶子)
1、在 Windows 上安装 GCC，需要到MinGW 的主页 www.mingw.org，进入 MinGW 下载页面，下载最新版本的 MinGW 安装程序；

2、添加环境变量：选择计算机—属性---高级系统设置---环境变量，在系统变量中找到 Path 变量，在后面加入 min-gw的安装目录，如 D:\MinGw\bin；

3、命令行安装：在开始菜单中，点击"运行"，输入 cmd,打开命令行:输入 mingw-get,如果弹出 MinGw installation manager 窗口，说明安装正常。此时，关闭 MinGw installation manager 窗口，否则接下来的步骤会报错；

4、在cmd中输入命令 mingw-get install gcc,等待一会，gcc 就安装成功了。如果想安装 g++,gdb,只要输入命令 mingw-get install g++ 和 mingw-get install gdb；

5、编译：输入gcc hello.c，即可生成exe文件，双击运行查看效果。注意如果你的hello.c在别处，请写相对地址或绝对地址，如：gcc C:\hello.c。

Linux篇：
最简单的方法就是：yum install gcc -y，等待安装完毕即可。

### 0x03 小结
编程有风险，入坑需谨慎。

![Image text](https://raw.githubusercontent.com/gitcsw/blogs/master/catalogue/c/images/00.png)
