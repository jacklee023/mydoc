
## 1. 安装git服务器所需软件
### 1.1 安装git-core/openssh-server/openssh-client
`git-core`是git版本控制的核心软件。
安装`openssh-server`和`openssh-client`是由于 git 需要通过 ssh协议在服务器与客户端之间传输文件,命令如下：
```
sudo apt-get update #可选
sudo apt-get install git-core openssh-server openssh-client
```

### 1.2 安装Python的setuptools和gitosis ，
由于gitosis安装需要依赖Python的一些工具,命令如下：
```
sudo apt-get install python-setuptools
```

### 1.3 安装gitosis
#### 1.3.1 初始化git用户信息
```
git config --global user.name "xxx"
git config --global user.email "yyy"
```
#### 1.3.2 获取gitosis
```
git clone https://github.com/res0nat0r/gitosis.git
```
#### 1.3.3 安装gitosis
```
cd gitosis
sudo python setup.py install
```

## 2.创建git管理员账户、配置git

### 2.1创建一个账户（git）作为git服务器的管理员
```
sudo useradd -m git
sudo passwd git
```
### 2.2 创建一个项目仓库存储点，并设置权限
```
sudo mkdir /home/gitrepository
sudo chown git:git /home/gitrepository/
sudo chmod 700 /home/gitrepository/
```

### 2.3 创建link
由于gitosis默认状态下将仓库放在用户的repositories目录下，添加一个链接，指向连接仓库的项目/home/gitrepository
```
sudo ln -s /home/gitrepository /home/git/repositories
#sudo ln -s /home/gitrepository /home/<username>/repositories #可选
```
### 2.4 创建ssh公钥
在git bash中执行
```
ssh-keygen -t rsa
```
### 2.5 初始化gitosis
```
sudo -H -u git gitosis-init < /tmp/xxx.pub
```
提示以下信息：
```
Initialized empty Git repository in /home/gitrepository/gitosis-admin.git/
Reinitialized existing Git repository in /home/gitrepository/gitosis-admin.git/
```
### 2.5 对post-update文件添加可执行权限
```
sudo chmod 755 /home/gitrepository/gitosis-admin.git/hooks/post-update
```
## 3.服务器上创建项目仓库与权限配置
### 3.1 使用git账户在服务器上创建一个目录
```
su git
cd /home/gitrepository
mkdir mytask.git
cd mytask.git
git init --bare # 最好加上--bare
exit
```
执行`git init --bare`Git会创建一个裸仓库，裸仓库没有工作区，因为服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的Git仓库通常都以.git结尾
最好使用 `git init --bare`而不是`git init`,否则可能遇到git 拒绝push的问题,可以通过配置`git/config`来解决
```
[receive]
denyCurrentBranch = ignore
```
参考[[Linux] Git: push 出错的解决 master -> master (branch is currently checked out)](https://www.cnblogs.com/abeen/archive/2010/06/17/1759496.html)
### 3.2 配置gitosis
#### 3.2.1 在客户端上clone `gitosis-admin.git`，打开git bash：
```
git clone git@<hostname>:repositories/gitosis-admin.git
```
#### 3.2.2 修改gitosis.conf
==TODO==

#### 3.2.3 提交修改到服务器
```
git add .
git commit -m "add new"
git push origin master
```

#### 3.2.4 重启sshd服务
```
sudo /etc/init.d/ssh restart
```

## 4.开始使用
### 4.1 在Central(远程仓库) init 环境
```
su git
cd /home/gitrepository/
mkdir mygit
cd mygit
git init --bare
```
### 4.2 Windows下使用git bash clone
```
git clone git@<hostname>:repositories/mygit
#修改文件，参考3.2.3节提交修改
```
### 4.3 云服务器端直接clone
```
git clone git@localhost:repositories/mygit
#修改文件，参考3.2.3节提交修改
```

## 5 配置权限，免密码clone/push
### 5.1 服务器端设置权限
```
chown -R git:git git#设置git文件夹所有用户归git用户
```
### 5.2 服务器端其他账号产生公钥文件并完成配置
```
ssh-keygen -t rsa -C "mail@gmail.com" #没试过-C 不写行不行
```
默认保存位置在`.ssh/id_rsa.pub`(命令执行完会提示)
将其中内容粘贴到`/home/git/.ssh/authorized_keys`即可
### 5.3 PC端产生公钥文件并完成配置
用gitbash执行5.2节命令并操作即可

此时PC端和服务器其他账号都可以免密码进行clone/push等操作


## x.待完成
1.	~~添加公钥有问题，每次clone/push仍需要输入git密码~~
2.	git clone做个alias
3.	教程说git clone git@<hostname> 不需要加绝对路径，但是试出来不一样，待查
4.	参考第6节 *[参考资料]* 完成3.2.2

## 6.参考资料
1.  [【腾讯云的1001种玩法】Ubuntu Server搭建 Git 服务器实测版](https://cloud.tencent.com/developer/article/1004848)   
2.  [Git服务器Gitosis安装设置](https://wiki.ubuntu.com.cn/Git%E6%9C%8D%E5%8A%A1%E5%99%A8Gitosis%E5%AE%89%E8%A3%85%E8%AE%BE%E7%BD%AE)   
3.  [Gitosis配置手记](http://debugo.com/gitosis/)
4.  [服务器上的 Git - Gitosis](https://git-scm.com/book/zh/v1/%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E7%9A%84-Git-Gitosis)
5.  [服务器上的 Git - 在服务器上搭建 Git](https://git-scm.com/book/zh/v2/%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E7%9A%84-Git-%E5%9C%A8%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E6%90%AD%E5%BB%BA-Git#r_git_on_the_server)
6.  [腾讯云上怎么安装git服务器？](http://bbs.qcloud.com/thread-10037-1-1.html)
7.  [【Git】【SSH】搭建git服务器以及利用SSH免密码clone](https://zhuanlan.zhihu.com/p/30643235)
