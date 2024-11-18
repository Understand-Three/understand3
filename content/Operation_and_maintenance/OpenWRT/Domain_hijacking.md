---
title: 域名劫持
aliases:
  - 域名劫持
draft: true
---
把 `test.cn` 的泛域名都解析到 `192.168.1.1`

# 方法一：

打开路由器控制台， http://192.168.5.1 

`网络` > `DHCP/DNS` 

最下方 `自定义挟持域名`

![[../../Images/openwrt域名劫持.png]]


# 方法二：

https://www.right.com.cn/forum/thread-8285663-1-1.html

```bash
vim /etc/dnsmasq.conf
```

在里面添加一行

```bash
address = /test.cn/192.168.1.1  
```

内网的设备 `dns` 地址都要填路由器的，不然劫持不了 ，或者有些固件直接会劫持53端口，那样就不用管了

编辑完保存以后记得重启一下服务  

```bash
service dnsmasq restart  
```

不然不生效