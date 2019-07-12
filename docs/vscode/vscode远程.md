# Vscode 访问修改远程文件

使用vscode访问和修改远程文件，分三步实现：在远程linux机器上安装rmate；在本地windows上安装openssh；在vscode中安装扩展remote vscode。

1、 在远程linux机器上安装rmate

rmate有很多中语言版本，这里用的是python的版本。github地址:https://github.com/sclukey/rmate-python

下载安装比较简单，在linux中执行以下命令即可
```
wget https://raw.githubusercontent.com/sclukey/rmate-python/master/bin/rmate
chmod +x ./rmate
mv ./rmate /usr/local/bin/rmate
```

2、在本地window中安装openssh

github地址：https://github.com/openssl/openssl/blob/master/INSTALL

这个是需要自己编译的，推荐直接利用window版的安装包：https://www.mls-software.com/opensshd.html

可以直接运行 ssh-keygen -t rsa 命令生成密钥对，一般默认的文件夹会在当前用户目录下的.ssh文件夹中。在windows的命令行中实现对远程linux的免密码登录，和在linux系统中的方式是一样的，将windows中生成的公钥id_rsa.pub文件追加到所用的linux登录用户的.ssh目录中的authorized_key文件中即可。

要使authorized_key生效，需要需要对sshd_config文件进行修改，主要是以下三项，取消注释即可

``` vim /etc/ssh/sshd_config```
```
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile      .ssh/authorized_keys
```
之后，执行 service sshd restart 命令重启sshd服务
```
service sshd restart
# 之后
cat id_rsa.pub >> authorized_keys
# 注意文件的路径
# 注意的是，如果使用的linux登录用户不是root用户，需要修改以下.ssh文件夹以及authorized_key文件的权限，否则是无法实现免密码登录的

chmod 700 .ssh
cd .ssh/
chmod 600 authorized_keys
```

3、安装remote vscode扩展

扩展地址：https://marketplace.visualstudio.com/items?itemName=rafaelmaiolla.remote-vscode

安装完成后，面板中点击Start Server，启动服务（这一步是必须的）



之后打开终端（【查看】——【集成终端】），输入以下命令：

```
ssh -R 52698:127.0.0.1:52698 登录linux用户名@linux计算机ip地址
ssh -R 52698:127.0.0.1:52698 learn@192.168.1.215
ssh -R 52698:127.0.0.1:52698 learn@192.168.1.215 -p 2159
```
登陆上linux服务器之后
```
rmate -p 52698 linux中的文件名称
```

插件自启动：remote vscode插件自动加载：文件>首选项>设置，搜索remote

配置doskey快速登陆

创建文件C:\cmd-alias.bat
```
doskey login=ssh -R 52698:127.0.0.1:52698 ubuntu@118.24.102.42
```

使用Win+R，输入regedit进入注册表，找到HKEY_LOCAL_MACHINE\Software\Microsoft\Command Processor，右键新建，字符串值，名为AutoRun，值为C:\cmd-alias.bat，保存退出