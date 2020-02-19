# Windows安装OpenSSH服务

## [参考文档](https://www.jianshu.com/p/6e5bc39d386e)

## 简介

该安装是使用微软官方的解决方案，基于PowerShell的*OpenSSH*

[安装包下载链接][link1]

## 安装步骤

> 1. 进入安装包下载链接下载相应的安装包，解压。
> 2. 打开cmd，进入安装包的解压目录\*\OpenSSH，并执行如下`命令`安装OpenSSH服务**（注意使用管理员模式运行CMD）**
>
> ```CMD
> powershell.exe -ExecutionPolicy Bypass -File install-sshd.ps1
> ```
>
> 3. 设置服务自启动并启动服务
>
> ``` CMD
> sc config sshd start=auto
> net start sshd
> ```

到此服务已经安装完毕，默认端口一样是22，默认用户名密码为Window账户名和密码，当然防火墙还是要设置对应端口允许通讯

## 修改设置

通常linux下会修改ssh_config文件来修改ssh配置，但在安装目录并没有发现这个文件，查阅官方wiki后发现，原来是在**C:\ProgramData\ssh**目录下*（此目录为隐藏目录）*

> 端口号：Port 22
>
> 密钥访问：PubkeyAuthentication yes
>
> 密码访问：PasswordAuthentication no
>
> 空密码：PermitEmptyPasswords no

然后进入**C:\Users\账户名\.ssh**目录，创建**authorized_keys**公钥文件*（也可在ssh_config修改路径）*

设置完成后重启sshd服务，接下来就可以使用Xshell等工具使用密钥连接了~

[link1]:https://github.com/PowerShell/Win32-OpenSSH/releases

