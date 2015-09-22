# auto_ssh_tools

这是一套用shell编写的自动登录服务器、自动进行scp操作的工具，可以免去大家手动输入密码的烦恼。

# 前提条件

使用本工具前，你需要在机器上安装 `expect`。

# 如何使用

1. 编写一个像下面这样格式的配置文件：

        192.168.0.122 root your_password 22

    配置文件中，第一列是你服务器的域名或者ip地址，第二列是你的ssh登录用户名，第三列是你的登录密码，第四列是服务器的ssh端口号。
    
    保存这个配置文件，比如我将它保存在 `servers/demo_svr`。
    
2. 进行自动登录时，你只需要进入到 `auto_ssh_tool/` 目录，然后敲下如下命令：

        ./goto servers/demo_svr

    然后你会发现你已经成功登录到你的服务器上。
    
    > goto 的第一个参数为配置文件路径。

3. If you just want to login to your server to execute a command and then exit, you can use `gotocmd` instead:
    
         ./goto servers/demo_svr 'ls -ltr'

---
> **实现原理：**
> 
> `goto` 工具会自动在`/tmp`下生成一个`expect`脚本，以随机名称命名，然后它会调用`expect`执行自己生成的那个脚本。

>  `auto_ssh_tool/` 目录下的其他工具也是用相同的方式实现的。
    
# 自动scp传输文件

如果你需要用scp从本机传送文件到其他服务器，将其他服务器的文件传送到本机， `pullfile` 和 `pushfile` 工具就可以大显身手了。

从另一台服务器拉取一个文件，用下面的命令：

    ./pullfile servers/demo_svr /root/file_to_pull.txt /tmp/

这样另一台服务器上的 `/root/file_to_pull.txt` 就会被scp到你本机的 `/tmp` 目录下。

从本机推送一个文件到另一台服务器，用下面的命令:

    ./pushfile servers/demo_svr /tmp/file_to_push.txt /root/

这样你本机上的 `/tmp/file_to_push.txt` 就会被scp到另一台机器上的 `/root/` 目录下。



----

----

# English (Manually Translated)
-----

# auto_ssh_tools

This is a suit of tools written in shell for automatic ssh and scp, without entering passwords manually. 

# Pre-equisitions

To use the tools, you need to install `expect`.  

# How to use

1. Write a config file with only one line like this:

        192.168.0.122 root your_password 22

    The first column is the domain name or ip of your linux server. The second and third columns are user name and password that you login with, the last column is the port number that your ssh server listening on.
    
    Save this file, for example I save it into `servers/demo_svr`.
    
2.    To do the automatic login, just goto the `auto_ssh_tool/` directory, and type the command:

        ./goto servers/demo_svr


    Then you will find you've successfully logged into your server.

    > The first command line param of `goto` is the config file path.

3.    If you just want to login to your server to execute a command and then exit, you can use `gotocmd` instead:
    
         ./goto servers/demo_svr 'ls -ltr'

---
> **How this is done:**
> 
>    The `goto` script generates an expect script in `/tmp` with a random filename,  then it calls expect to execute the  expect script to complete the login.

>    Other tools in `auto_ssh_tool/` are implemented in the same way. 
    
-----

# Automatic scp file transfer

If you need to pull file from your remote server or push local file to your remote server via scp, the `pullfile` and `pushfile` tools will be useful.

To pull a file, use command like this:

    ./pullfile servers/demo_svr /root/file_to_pull.txt /tmp/

Then the `/root/file_to_pull.txt` on the remote server will be transfered to your local directory `/tmp` via scp.

To push a file, use command like this:

    ./pushfile servers/demo_svr /tmp/file_to_push.txt /root/

Then the `/tmp/file_to_push.txt` in your local `/tmp` directory will be transfered to the remote server into the `/root/` directory.
