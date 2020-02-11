# frp+teamviewer

下载frp客户端（https://github.com/fatedier/frp/releases）

服务端配置文件frps.ini内容如下
```
[common]
bind_port = 7002

```
运行以下命令启动服务
```
frps -c frps.ini
```

被控机上配置frpc.ini内容如下
```
[common]
server_addr = 119.23.40.38
server_port = 7002

[rdp]
type = tcp
local_ip = 127.0.0.1
local_port = 5938
remote_port = 5938
```
运行以下命令启动服务
```
frpc -c frpc.ini
```

远程双方teamviewer都应设置Incomming Lan Connection为accept，控制机teamviewer直接输入119.23.40.38即可远程。

# TeamViewer 的端口
以下是 TeamViewer 需要使用的端口：

TCP/UDP 端口 5938
TeamViewer 倾向于通过 端口5938 进行对外的 TCP 和 UDP 连接 — 这是TeamViewer的主要端口，并且 TeamViewer 在使用此端口时具有最佳性能。您的防火墙应至少允许使用此端口。

TCP 端口 443
如果 TeamViewer 无法通过端口 5938 进行连接，接下来会尝试通过 TCP 端口 443 进行连接。

但是，Android、iOS、Windows Mobile 和 BlackBerry 移动端上运行的TeamViewer不使用端口 443。

注意: 我们在管理控制台中创建的自定义模块也使用端口 443。如果您要通过群组策略部署自定义模块，则需要确保您要部署的计算机上的端口 443 打开。端口 443 还有其他用途，包括 TeamViewer 更新检查。

TCP 端口 80
如果 TeamViewer 无法通过端口 5938 或 443 进行连接，则会尝试通过 TCP 端口 80 进行连接。由于会产生了额外的开销（Overhead），并且如果连接断开也不会自动重新连接，通过此端口的连接速度比端口 5938 或 443 慢，可靠性也较低。因此，端口 80 仅作为最后备用选择。

Android、Windows Mobile 和 BlackBerry 上运行的TeamViewer不使用端口 80。但是，如果需要，我们的 iOS 应用程序可使用端口 80。