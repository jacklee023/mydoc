# frp 内网穿透配置

[官方说明](https://github.com/fatedier/frp)

# 服务器端配置：
1.  登录服务器，在 Release页面 下载自己服务器对应版本 Frp
```
wget https://github.com/fatedier/frp/releases/download/v0.12.0/frp_0.12.0_linux_amd64.tar.gz
```
2. 使用 tar 指令解压 tar.gz 文件
```
tar -zxvf frp_0.12.0_linux_amd64.tar.gz
```
3. 进入 frp 目录
```
cd frp_0.12.0_linux_amd64
```
4. 删除不必要的客户端文件
```
rm -f frpc frpc_full.ini frpc.ini
```
> 版本不同可能稍有差异   
> frpc 为客户端文件  
> frps 为服务器端文件

5. 配置服务器端文件

```
[common]
bind_port = 7000
vhost_https_port = 8081
vhost_http_port = 8080
```

6. 后台运行frpc
```
nohup ./frps -c frps.ini  &
```

# 客户端配置
1. SSH 登录群晖 NAS （群晖必须开启 ssh）
2. 下载 Frp, 删除服务端文件。（因为和服务端配置一样，不再一一赘述。）
```
sudo -i // 切换 root 用户
wget https://github.com/fatedier/frp/releases/download/v0.12.0/frp_0.12.0_linux_386.tar.gz 
tar -zxvf  frp_0.12.0_linux_386.tar.gz
cd frp_0.12.0_linux_386
rm -f frps frps_full.ini frps.ini
```
3. 编辑 frpc.ini 文件（客户端配置文件）

```
[common]
server_addr = 118.24.102.42
server_port = 7000

[ssh]
type = tcp
local_ip = 192.168.1.8
local_port = 42
remote_port = 6000

[web]
type = https
local_port = 501
remote_port = 8081
privilege_mode = true
custom_domains = www.pyvlyf.club

[http]
type = http
local_port = 500
remote_port = 8080
privilege_mode = true
custom_domains = www.pyvlyf.club
```

4.后台运行frps
```
#!/bin/sh
nohup frpc -c frpc.ini &
```

5.设置NAS 开机自动启动frp

<!-- ![image](https://raw.githubusercontent.com/PhoYttVan/Image-Hosting-/master/frp%20boot%20nas%20setting.png) -->
![image](../pic/frp%20boot%20nas%20setting.png)