# Nano Pi
玩转NanoPi R2S

中文维基 [NanoPi R2S/zh](http://wiki.friendlyarm.com/wiki/index.php/NanoPi_R2S/zh)

英文维基 [NanoPi R2S](http://wiki.friendlyarm.com/wiki/index.php/NanoPi_R2S)

SD卡自带FriendlyCore

FriendlyARM   NanoPi R2S 的核心  Rockchip RK3328 是 armv8 架构，所有智能用Openwrt官方的snapshot，还是刷FriendlyWrt吧。

## 基本使用

在电脑浏览器上输入以下网址即可进入FriendlyWrt管理页面:

- http://friendlywrt/
- http://192.168.2.1/

升级所有的软件包

```sh
opkg update
opkg list-upgradable | cut -f 1 -d ' ' | xargs opkg upgrade 
```





### 建议的安全性设置

以下设置事项非常建议在将 NanoPi-R2S 接入互联网之前完成，因为在空密码或弱密码的状态下将NanoPi-R2S接入互联网，极易受到网络攻击。

- 设置一个安全的密码

进入 系统->管理权 界面设置密码。

- 禁止从wan访问ssh，更换端口

进入 系统->管理权->SSH访问，将接口限制为 lan，将端口设置为其他非常用端口，例如 23333。

- 只允许本地设备访问luci

编辑 /etc/config/uhttpd，将原来的0.0.0.0和[::]地址改为本地lan的地址，例如：

```
	# HTTP listen addresses, multiple allowed
	list listen_http	192.168.2.1:80
	list listen_http	[fd00:ab:cd::1]:80
 
	# HTTPS listen addresses, multiple allowed
	list listen_https	192.168.2.1:443
	list listen_https	[fd00:ab:cd::1]:443
```

完成后重启服务：

```
/etc/init.d/uhttpd restart
```



## OpenVPN client using LuCI

https://openwrt.org/docs/guide-user/services/vpn/openvpn/client-luci



