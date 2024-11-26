---
title: 使用 OpenVPN 搭建组网
pubDatetime: 2024-03-29T03:03:00.000Z
tags:
  - 服务器
---

首先在服务器上运行一键安装脚本

```
wget https://git.io/vpn -O openvpn-install.sh && bash openvpn-install.sh
```

如果是大陆服务器的话，可能会无法下载脚本的情况，可以在[GitHub][1]下载后上传到服务器`root`文件下，然后运行

```
bash openvpn-install.sh
```

```
# 此服务器位于NAT之后。公共IPv4地址或主机名是什么？（这里输入服务器的公网IP）
This server is behind NAT. What is the public IPv4 address or hostname?
Public IPv4 address / hostname [47.240.162.161]:

# 您希望OpenVPN连接使用哪种协议（这里选择UDP）
Which protocol do you want for OpenVPN connections?
   1) UDP (recommended)
   2) TCP
Protocol [1]:

# 你想让OpenVPN监听哪个端口？（这里我按默认的）
What port do you want OpenVPN listening to?
Port [1194]:

# 您想将哪个DNS用于VPN？（这里我按默认的）
Which DNS do you want to use with the VPN?
   1) Current system resolvers
   2) 1.1.1.1
   3) Google
   4) OpenDNS
   5) Verisign
DNS [1]:

# 最后，告诉我客户端证书的名称（这个是客户端用户名称）
Finally, tell me a name for the client certificate.
Client name [client]:
```

安装完成后，然后打开`/etc/openvpn/server/server.conf`

删除

```
push "redirect-gateway def1 bypass-dhcp"
push "dhcp-option DNS 100.100.2.136"
push "dhcp-option DNS 100.100.2.138"
```

添加一行

```
client-to-client
```

完整配置文件（这里的IP根据实际情况即原配置文件）

```
local 172.17.53.81
port 1194
proto udp
dev tun
ca ca.crt
cert server.crt
key server.key
dh dh.pem
auth SHA512
tls-crypt tc.key
topology subnet
server 10.8.0.0 255.255.255.0
ifconfig-pool-persist ipp.txt
client-to-client
keepalive 10 120
cipher AES-256-CBC
user nobody
group nobody
persist-key
persist-tun
status openvpn-status.log
verb 3
crl-verify crl.pem
explicit-exit-notify
```

然后打开`/etc/openvpn/server/client-common.txt`
删除

```
ignore-unknown-option block-outside-dns
block-outside-dns
```

继续执行 `openvpn-install.sh` 可以创建、删除用户，客户端用户的配置文件位于`/root/xxx.ovpn`

```
bash openvpn-install.sh
```

客户端下载地址：
[Windows][2]
[Android][3]

[1]: https://github.com/Nyr/openvpn-install
[2]: https://openvpn.net/community-downloads/
[3]: https://github.com/schwabe/ics-openvpn
