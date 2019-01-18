# PHP运行模式和原理

### PHP常见的运行模式
---
- CGI（通用网关接口 - Common Gateway Interface)
- FastCGI（常驻型CGI Long-Live-CGI)
- Web模块模式（Apache等Web服务器运行的模式)
- CLI（命令行运行 - Comman-Line-Interface)

### CGI 模式
---
CGI即通用网关接口(Common Gateway Interface)，它是一段程序, 通俗的讲CGI就象是一座桥，把网页和WEB服务器中的执行程序连接起来，它把HTML接收的指令传递给服务器的执行程序，再把服务器执行程序的结果返还给HTML页。CGI 的跨平台性能极佳，几乎可以在任何操作系统上实现。 CGI已经是比较老的模式了，这几年都很少用了。

每有一个用户请求，都会先要创建cgi的子进程，然后处理请求，处理完后结束这个子进程，这就是fork-and-execute模式。 当用户请求数量非常多时，会大量挤占系统的资源如内存，CPU时间等，造成效能低下。所以用cgi方式的服务器有多少连接请求就会有多少cgi子进程，子进程反复加载是cgi性能低下的主要原因。

如果不想把 PHP 嵌入到服务器端软件（如 Apache）作为一个模块安装的话，可以选择以 CGI 的模式安装。或者把 PHP 用于不同的 CGI 封装以便为代码创建安全的 chroot 和 setuid 环境。这样每个客户机请求一个php文件，Web服务器就调用php.exe（win下是php.exe,linux是php）去解释这个文件，然后再把解释的结果以网页的形式返回给客户机。 这种安装方式通常会把 PHP 的可执行文件安装到 web 服务器的 cgi-bin 目录。CERT 建议书 CA-96.11 建议不要把任何的解释器放到 cgi-bin 目录。

这种方式的好处是把web server和具体的程序处理独立开来，结构清晰，可控性强，同时缺点就是如果在高访问需求的情况下，cgi的进程fork就会成为很大的服务器负担，想 象一下数百个并发请求导致服务器fork出数百个进程就明白了。这也是为什么cgi一直背负性能低下，高资源消耗的恶名的原因。


### FastCGI 模式
---
fast-cgi 是cgi的升级版本，FastCGI 像是一个常驻 (long-live) 型的 CGI，它可以一直执行着，只要激活后，不会每次都要花费时间去 fork 一次 (这是 CGI 最为人诟病的 fork-and-execute 模式)。 

**FastCGI的工作原理:**

- Web Server启动时载入FastCGI进程管理器【PHP的FastCGI进程管理器是PHP-FPM(php-FastCGI Process Manager)】（IIS ISAPI或Apache Module);

- FastCGI进程管理器自身初始化，启动多个CGI解释器进程 (在任务管理器中可见多个php-cgi.exe)并等待来自Web Server的连接。

- 当客户端请求到达Web Server时，FastCGI进程管理器选择并连接到一个CGI解释器。Web server将CGI环境变量和标准输入发送到FastCGI子进程php-cgi。

- FastCGI子进程完成处理后将标准输出和错误信息从同一连接返回Web Server。当FastCGI子进程关闭连接时，请求便告处理完成。FastCGI子进程接着等待并处理来自FastCGI进程管理器（运行在 WebServer中）的下一个连接。在正常的CGI模式中，php-cgi.exe在此便退出了。


在CGI模式中，你可以想象 CGI通常有多慢。每一个Web请求PHP都必须重新解析php.ini、重新载入全部dll扩展并重初始化全部数据结构。使用FastCGI，所有这些都只在进程启动时发生一次。一个额外的好处是，持续数据库连接(Persistent database connection)可以工作。

**FastCGI的优点:**

- 从稳定性上看, fastcgi是以独立的进程池运行来cgi,单独一个进程死掉,系统可以很轻易的丢弃,然后重新分 配新的进程来运行逻辑.

- 从安全性上看,Fastcgi支持分布式运算. fastcgi和宿主的server完全独立, fastcgi怎么down也不会把server搞垮.

- 从性能上看, fastcgi把动态逻辑的处理从server中分离出来, 大负荷的IO处理还是留给宿主server, 这样宿主server可以一心一意作IO,对于一个普通的动态网页来说, 逻辑处理可能只有一小部分, 大量的图片等静态 


**FastCGI的缺点:**

用FastCGI模式更适合生产环境的服务器。但对于开发用机器来说就不太合适。因为当使用 Zend Studio调试程序时，由于 FastCGI会认为 PHP进程超时，从而在页面返回 500错误。这一点让人非常恼火，所以我在开发机器上还是换回了 ISAPI模式。


### Model 模式
---

模块模式是以mod_php5模块的形式集成，此时mod_php5模块的作用是接收Apache传递过来的PHP文件请求，并处理这些请求，然后将处理后的结果返回给Apache。如果我们在Apache启动前在其配置文件中配置好了PHP模块（mod_php5）， PHP模块通过注册apache2的ap_hook_post_config挂钩，在Apache启动的时候启动此模块以接受PHP文件的请求。

除了这种启动时的加载方式，Apache的模块可以在运行的时候动态装载，这意味着对服务器可以进行功能扩展而不需要重新对源代码进行编译，甚至根本不需要停止服务器。我们所需要做的仅仅是给服务器发送信号HUP或者AP_SIG_GRACEFUL通知服务器重新载入模块。但是在动态加载之前，我们需要将模块编译成为动态链接库。此时的动态加载就是加载动态链接库。 Apache中对动态链接库的处理是通过模块mod_so来完成的，因此mod_so模块不能被动态加载，它只能被静态编译进Apache的核心。这意味着它是随着Apache一起启动的。


### CLI 模式
---
cli是php的命令行运行模式