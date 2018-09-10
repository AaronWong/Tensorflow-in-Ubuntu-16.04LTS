1. wegt 下载 <https://github.com/fatedier/frp/releases>

2. 新建目录mkdir -p /usr/local/frp，上传frp_0.13.0_linux_amd64.tar.gz至linux服务器该目录下

3. 解压tar -zxvf  frp_0.13.0_linux_amd64.tar.gz

4. 进入解压目录cd frp_0.13.0_linux_amd64，这里主要关注4个文件，分别是frpc、frpc.ini和frps、frps.ini，前者两个文件是客户端所关注文件，后者两个文件是服务端所关注两个文件。

5. 配置服务端（公网服务器），首先删掉frpc、frpc.ini两个文件，然后再进行配置，vi ./frps.ini，

```
[common]
bind_port = 7000           #与客户端绑定的进行通信的端口
```

~~保存然后启动服务./frps -c ./frps.ini，这是前台启动，后台启动命令为nohup ./frps -c ./frps.ini &~~

$ nohup /usr/local/frp/frps -c /usr/local/frp/frps.ini &

为了不每次启动都需手动输入一遍，设置为开机启动。在/etc/rc.local中添加上边的命令，注意在exit 0之前。

6. 配置客户端（内网服务器），首先删掉frps、frps.ini两个文件,然后再进行配置，vi ./frpc.ini

```
[common]
server_addr = 120.56.37.48   #公网服务器ip
server_port = 7000            #与服务端bind_port一致
 
#公网通过ssh访问内部服务器
[ssh]
type = tcp              #连接协议
local_ip = 192.168.3.48 #内网服务器ip
local_port = 22         #ssh默认端口号
remote_port = 222      #自定义的访问内部ssh端口号
 
#公网访问内部web服务器以http方式
[web]
type = http         #访问协议
local_port = 8081   #内网web服务的端口号
custom_domains = repo.iwi.com   #所绑定的公网服务器域名，一级、二级域名都可以
```

~~保存然后执行./frpc -c ./frpc.ini启动，这是前台启动，后台启动命令为nohup ./frpc -c ./frpc.ini &~~

$ nohup /usr/local/frp/frpc -c /usr/local/frp/frpc.ini &

为了不每次启动都需手动输入一遍，设置为开机启动。在/etc/rc.local中添加上边的命令，注意在exit 0之前。
