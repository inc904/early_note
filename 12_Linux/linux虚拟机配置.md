## 用户密码


个人用户：

inc904
0904.com

root用户：

root
0904


## IP 地址

宿主机iP：

192.168.1.100

机器1：

ip： 192.168.221.4

机器2：
192.168.221.3

## 分配 静态ip 地址：

工具 dhclint，分配一个ip地址；拿到ip地址后，写成静态。

`vim /etc/sysconfig/network-scripts/ifcfg-` 

```
修改内容：
BOOTPROTO:dhcp  // dhcp => static
ONBOOT:no // no =>yes
添加：
IPADDR: 生成的IP  // ip 地址
NETMASK: 255.255.255.0 // 子网掩码
GATEWAY：192.168.221.2 // 网关
DNS1:119.29.29.29  // 公网的DNS地址,这里用的腾讯的
```
重启网卡：

`systemctl restart network.service`