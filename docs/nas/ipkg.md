群晖内建Linux系统很多常用包没有安装，而且常用的apt-get在群晖系统下也无法使用，经过查找发现ipkg可以替代apt-get,下面介绍群晖安装ipkg的方法
## 1.   ssh登录到群晖
> 待完善

## 2.   查询自己的机器使用何种CPU
在该网址查询[Synology NAS 使用哪种 CPU？](https://www.synology.com/zh-cn/knowledgebase/DSM/tutorial/General/What_kind_of_CPU_does_my_NAS_have)


## 3.   下载对应的安装命令
在[该网址](http://ipkg.nslu2-linux.org/optware-ng)找到对应的安装命令
> 并不是太懂CPU型号与估计版本的对应关系
经过试验DS116可以使用[该版本](http://ipkg.nslu2-linux.org/optware-ng/bootstrap/buildroot-armv5eabi-ng-legacy-bootstrap.sh),使用wget命令下载
```
wget http://ipkg.nslu2-linux.org/optware-ng/bootstrap/buildroot-armv5eabi-ng-legacy-bootstrap.sh
```
## 4.   执行安装命令
```
sh buildroot-armv5eabi-ng-legacy-bootstrap.sh
```
## 5.   测试ipkg是否安装成功
```
ipkg update
ipkg install <pkg name>
```
## 6.   支持的package列表
[package列表](http://ipkg.nslu2-linux.org/optware-ng/buildroot-armv5eabi-ng-legacy/Packages.html)

## 7.   故障排除经验
### 7.1 OPT 下无法创建目录解决方法 [来源](https://blog.csdn.net/jekkihun/article/details/8547456)
#### 现象：
```
...
Installing wget...
/opt/bin/ipkg: error while loading shared libraries: /opt/lib/libipkg.so.0: ELF file OS ABI invalid
```
#### 解决办法：
```
rm -rf /opt/*
umount /opt
edit /etc/init.d/rcS to remove optware startup (leaving it there is fine too)
```

### 7.2 重复安装的错误提示
#### 现象：
```
···
Backup your configuration settings, then type:
  rm -rf /volume1/@optware
  rm -rf /usr/lib/ipkg
This will remove all existing optware packages.

You must *reboot* and then restart the bootstrap script.
```
#### 解决办法：
如提示，删除指定目录即可，建议备份
```
  rm -rf /volume1/@optware
  rm -rf /usr/lib/ipkg
```

### 7.3 使用了错误的安装命令
#### 现象:
```
...
Installing wget...
/opt/bin/ipkg: error while loading shared libraries: /opt/lib/libipkg.so.0: ELF file OS ABI invalid
```
提示`ELF file OS ABI invalid`说明编译的环境不兼容
#### 解决办法：
使用正确的安装命令

### 7.4 无法直接调用ipkg
#### 现象:
无法直接调用，必须输入全路径`/opt/bin/ipkg`才能使用
#### 解决办法：
将`/opt/bin`添加到环境变量
```
export PATH=/opt/bin:$PATH
```