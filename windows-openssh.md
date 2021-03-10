微软官方的解决方案：

基于PowerShell的OpenSSH：https://github.com/PowerShell/Win32-OpenSSH/releases

详细说明可以参考Github的Wiki，这里简单说下安装步骤：

安装步骤：
1、进入链接下载最新 OpenSSH-Win64.zip（64位系统），解压至C:\Program Files\OpenSSH

2、打开cmd，cd进入C:\Program Files\OpenSSH（安装目录），执行命令：

powershell.exe -ExecutionPolicy Bypass -File install-sshd.ps1

3、设置服务自动启动并启动服务：

sc config sshd start= auto   #执行失败无妨，可以在服务管理手动设置

net start sshd

到此服务已经安装完毕，默认端口一样是22，默认用户名密码为Window账户名和密码，当然防火墙还是要设置对应端口允许通讯

修改设置：
通常linux下会修改ssh_config文件来修改ssh配置，但在安装目录并没有发现这个文件，查阅官方wiki后发现，原来是在C:\ProgramData\ssh目录下（此目录为隐藏目录）

端口号：Port 22

密钥访问：PubkeyAuthentication yes

密码访问：PasswordAuthentication no

空密码：PermitEmptyPasswords no

然后进入C:\Users\账户名\.ssh目录，创建authorized_keys公钥文件（也可在ssh_config修改路径）

设置完成后重启sshd服务，接下来就可以使用Xshell等工具使用密钥连接了~

踩过的坑：

如果配置秘钥无妨登录  注释C:\ProgramData\ssh\ssh.config 最后俩行解决。

