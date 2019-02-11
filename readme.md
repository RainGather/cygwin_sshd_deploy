## cygwin sshd 安装说明

cygwin中通过openssh可以安装sshd服务，其服务启动的时候需要一个Windows的账户权限，一般默认是会自动创建一个cyg_server，猜测sshd服务对Windows的访问最高权限即为该cyg_server用户的权限。

通过ssh连入时，需要的账户认证是基于Windows普通账户体系的认证，例如你有个Windows账户是xiaoming，密码是123，那么连入的命令应该为ssh xiaoming@host，密码为123。

## cygwin sshd 部署方法

1. 在windows下新建账户user1，设置密码
2. [下载](https://cygwin.com/install.html)并安装cygwin，在安装时选择openssh和需要安装的其它功能（例如rsync、vim等），并安装好
3. 以管理员权限运行cygwin.bat，输入ssh-host-config，一路yes
4. 在cygwin里输入mkpasswd > /etc/passwd
5. 在windows服务里启动CYGWIN sshd
6. 从client端用ssh user1@host测试是否部署成功
7. 完成！

## ssh自动接收局域网内陌生IP公匙设置

编辑ssh_config:
` vim /etc/ssh/ssh_config `
新增一条记录

``` shell
Host 192.168.*.*
    StrictHostKeyChecking no
```

其余内容与Host *一致，如有必要可以将Host * 的StrictHostKeyChecking改为no来达到自动接收所有ip的公匙

