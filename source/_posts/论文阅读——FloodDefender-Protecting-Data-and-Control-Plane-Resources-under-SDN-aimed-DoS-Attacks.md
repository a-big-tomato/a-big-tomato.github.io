---
title: >-
  论文阅读——FloodDefender-Protecting Data and Control Plane Resources under
  SDN-aimed DoS Attacks
date: 2018-03-14 17:40:33
tags:
- DoS
- SDN
- post-detection procedure;
---

论文题目:FloodDefender: Protecting Data and Control Plane Resources under SDN-aimed DoS Attacks 

来源:2017 INFOCOM

作者:GAO Shang, PENG Zhe, XIAO Bin, HU Aiqun, REN Kui

tag:DoS;SDN;post-detection procedure;

主要面向的问题为**缓解**在OpenFlow中SDN中特有的DoS攻击：

(即为检测到了DoS的攻击之后的操作)

1.如何在保持短时延、低缺失率正常包转发操作的同时有效处理table-miss的包更为合适

2.如何在流量开始阶段精确区分攻击流量，而不会消耗计算资源

<!-- more -->

主要贡献：

​		1.利用表缺失机制来防止带宽被用完

​		2.包过滤器来鉴别攻击流量，节约控制平面资源。

​		3.流规则管理消除交换机流表中无用的流实体


实验结果：实验同OpenFlow ,FloodGuard相比

节约了多余70%的软件带宽，20%的硬件带宽，引起不多于0.5%的CPU消耗用于处理攻击流量，同时，精确检测出超过96%的攻击流量，而只引起18ms的包延迟，以及在攻击下5%的包缺失率。

![FloodDefender 结构](https://note.youdao.com/yws/api/personal/file/WEBf70befcc5604bf63780176e26a66625c?method=download&shareKey=5284f89978a15d57f170840e231e5366)

具体过程：
1.attack detector module 检测攻击，一旦出现DoS攻击，其他module启动
2.table-miss engineering module 安装protecting rules将一些table-miss packets 绕道到邻居交换机。交换机收到detoured table-miss packets，会发送packet_in给控制器
3.当控制器收到packet_in时，packet filter 会接收这些信息，然后大致过滤出攻击流量。把过滤后的发给app
4.app处理这些包，决定actions和flow rules，前者给switch,后者会被flow rule management module 截获。
5.flow rule management module 基于截获的processing rule决定monitoring rules。monitoring rules 在 cache region,截获的processing rules放在flow table region. 
6.packet filter module 使用 intercepted and monitoring rules 的流量信息精确判定正常流量。如果一个processing flow entry 被视为合法的，就会被移到flow table region。monitoring rules和cache region 会被刷新来节约空间


