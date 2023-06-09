---
title: "我的N1旁路由设置方案之一"
date: 2020-03-12T13:23:59+08:00
description: "k2p作为主路由，N1作为旁路路由，该如何设置呢？"
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: inner
tocLevels: ["h2", "h3", "h4"]
tags:
- "路由器"
categories:
- "家庭组网"
series:
- "技术研究"
image: 
---

## k2p为主，N1作为旁路由
光猫已经改为桥接模式了

k2p的后台地址是 “192.168.123.1”

- k2p + N1 （padavan + F大 Openwrt29+）

- k2p作为pppoe拨号、AP

- N1接入其 Lan 口，作为旁路由

目的是，家中有特殊上网需要的设备，可以手动选择不同的网关（k2p不能特殊上网，N1可以）上网<br>
**而家人，或者客人连接上 wifi 时，则将是使用 k2p 默认分配 ip 地址，不会走 N1。**<br>

要特殊上网的设备，就要在连上k2p的 wifi 后<br>
自己修改静态地址，然后选择 192.168.123.2（N1）作为网关<br>
这样达到“分流”的效果（不过应该有更好【逼格】的方案 XD）

## k2p 开启 DHCP 服务
k2p 的内部网络（Lan）选项中，修改为如下<br>
这样设置，是为了等下把 N1 的后台地址设置为 “192.168.123.2”，给 N1 留个位置

![k2p后台修改DHCP](https://ae01.alicdn.com/kf/U122efd00562647dfb120f5591902d50dY.jpg)


# N1 的旁路由配置

## ① 后台管理地址修改 & 关闭 DNCP 服务
**下面的设置，最好在 N1 没有接入其他网关设备时进行
以免和自己的光猫后台地址冲突**

![N1后台修改管理地址-配置k2p作为网关](https://ae01.alicdn.com/kf/Ua3cc0e08d3e749829ee87a42ba952b47X.jpg)


## ②关闭 ipv6

![取消使用内置 IPV6 管理的勾选](https://ae01.alicdn.com/kf/U6aec0803e5064ffeb4f9f6dc7cc537133.jpg)

## ③选择以太网适配器接口

**我关闭了桥接接口**，但这一步不知道有没有什么影响（目前我这样用着没什么问题）

这一步一定要选中 “eth0”

否则，等下你保存配置后，是无法通过 “192.168.123.2” 进入后台的！！！

![取消桥接接口](https://ae01.alicdn.com/kf/U5921e4f582a94bb6a3e146bd9bd50352o.jpg)

可以每完成一个步骤后，先点击右下角保存（**不是保存并应用，有三个看清楚！**）

最后再一起保存并应用，这时候页面卡在当前页面，等待一两分钟

- 连接wifi后，不用修改为静态地址

- 浏览器输入 192.168.123.2

- 没问题的话应该能进入 N1 的后台了

## 自定义防火墙添加一条规则

**至于为什么要添加这一条指令，F 大在他的固件发布帖子中已经解释**

**H 大 padavan + F大opwrt（旁路由），需要添加，不然有影响**

**如果其他搭配方案，请参考F 大恩山论坛的帖子~**

[F大N1 OpenWrt 固件发布论坛](https://www.right.com.cn/FORUM/thread-981406-1-1.html)

> iptables -t nat -I POSTROUTING -o eth0 -j MASQUERADE

![添加防火墙自定义规则](https://ae01.alicdn.com/kf/U5733d4eb291d4d789130af1632c14d383.jpg)

然后重启防火墙就ok 了

## 最后

每个人设备状态不同

我的配置在自己的环境下测试，是没有问题的

如果大家遇到了问题，欢迎留言讨论

我也只是折腾了一段时间的菜鸟，特别有技术难度的问题

就还是别为难我了XD

难免有遗漏，欢迎批评指正

相互增进技术~