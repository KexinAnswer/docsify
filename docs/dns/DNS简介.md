## 概述

**域名系统**（英语：**D**omain **N**ame **S**ystem，缩写：**DNS**）是[互联网](https://zh.wikipedia.org/wiki/%E4%BA%92%E8%81%AF%E7%B6%B2)的一项服务。它作为将[域名](https://zh.wikipedia.org/wiki/%E5%9F%9F%E5%90%8D)和[IP地址](https://zh.wikipedia.org/wiki/IP%E5%9C%B0%E5%9D%80)相互[映射](https://zh.wikipedia.org/wiki/%E6%98%A0%E5%B0%84)的一个[分布式数据库](https://zh.wikipedia.org/wiki/%E5%88%86%E5%B8%83%E5%BC%8F%E6%95%B0%E6%8D%AE%E5%BA%93)，能够使人更方便地访问[互联网](https://zh.wikipedia.org/wiki/%E4%BA%92%E8%81%AF%E7%B6%B2)。DNS使用[TCP](https://zh.wikipedia.org/wiki/%E5%82%B3%E8%BC%B8%E6%8E%A7%E5%88%B6%E5%8D%94%E8%AD%B0)和[UDP](https://zh.wikipedia.org/wiki/%E7%94%A8%E6%88%B7%E6%95%B0%E6%8D%AE%E6%8A%A5%E5%8D%8F%E8%AE%AE)[端口](https://zh.wikipedia.org/wiki/TCP/UDP%E7%AB%AF%E5%8F%A3%E5%88%97%E8%A1%A8)53。当前，对于每一级域名长度的限制是63个字符，域名总长度则不能超过253个字符。顾名思义，DNS是一个记录域名和解析记录的关系的服务.

**目前的DNS系统**

- [BIND](https://zh.wikipedia.org/wiki/BIND)（Berkeley Internet Name Domain），使用最广的DNS软件
- [DJBDNS](https://zh.wikipedia.org/w/index.php?title=DJBDNS&action=edit&redlink=1)（Dan J Bernstein's DNS implementation）
- [MaraDNS](https://zh.wikipedia.org/w/index.php?title=MaraDNS&action=edit&redlink=1)
- [Name Server Daemon](https://zh.wikipedia.org/w/index.php?title=Name_Server_Daemon&action=edit&redlink=1)（Name Server Daemon）
- [PowerDNS](https://zh.wikipedia.org/wiki/PowerDNS)
- [Dnsmasq](https://zh.wikipedia.org/wiki/Dnsmasq)

## 发展历史

20世纪70年代 ARPAnet是一个只有几百台主机的小型，友好社区。所以只需要要host.txt文件 就可以包含连接到 ARPAnet的每台主机的名称地址的解析 人们树枝的UNIX的主机表(/etc/host)就是有hos.txt演变来的

随着树枝数量的新增 host.txt维护起来已经比较困难了

并且当ARPAnet 采用了TCP/IP协议后 用户出现激增 面临一下问题

- 流量和负载
- 名称冲突
- 一致性

根本问题在于host.txt文件扩展性不好

南加州大学信息科学研究所的Paul Mockapertris 负责设计这个新的系统 1984年 发布了 RFCs822和833。 目前RFC1034和1035已经被许多其他的RFC所扩充。

## 定义

### Zone

在DNS中，"区域"是指一个管理特定域名空间的部分。每个区域通常包含一组相关的DNS记录，用于管理特定域的资源记录。区域通常由域的管理员或托管提供商管理。每个区域都有一个主要的授权DNS服务器，负责管理该区域的DNS记录。

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/27d03606-1719-4428-ae31-5634ac9daca7/29b5692a-ffb5-456d-ac1f-fda86b2803c9/Untitled.png)

如图所示每个模块都是一个DNS服务，负责管理子树。DNS的管理就像一颗多叉树。

### HostName

主机名是一个标识特定网络设备的人类可读的名称。它通常是一个域名的一部分，用于识别特定主机或服务器。例如，在域名"[example.com](http://example.com/)"中，"www"是一个主机名，用于表示Web服务器。主机名与IP地址相对应，使人们能够通过名称而不是数字地址来访问网络资源。

### 解析

DNS解析是将域名转换为与之相关联的IP地址或其他资源记录的过程。它允许计算机在互联网上查找特定域名并找到与之关联的IP地址，从而能够建立连接。DNS解析是DNS系统的核心功能，使互联网用户能够使用人类可读的域名而不是记住复杂的IP地址。

- 主机记录（A记录）：[RFC 1035](https://tools.ietf.org/html/rfc1035)定义，A记录是用于名称解析的重要记录，它将特定的主机名映射到对应主机的IP地址上。
- 别名记录（CNAME记录）: [RFC 1035](https://tools.ietf.org/html/rfc1035)定义，CNAME记录用于将某个别名指向到某个A记录上，这样就不需要再为某个新名字另外创建一条新的A记录。
- IPv6主机记录（AAAA记录）: [RFC 3596](https://tools.ietf.org/html/rfc3596)定义，与A记录对应，用于将特定的主机名映射到一个主机的[IPv6](https://zh.wikipedia.org/wiki/IPv6)地址。
- 服务位置记录（SRV记录）: [RFC 2782](https://tools.ietf.org/html/rfc2782)定义，用于定义提供特定服务的服务器的位置，如主机（hostname），端口（port number）等。
- 域名服务器记录（NS记录） ：用来指定该域名由哪个DNS服务器来进行解析。 您注册域名时，总有默认的DNS服务器，每个注册的域名都是由一个DNS域名服务器来进行解析的，DNS服务器NS记录地址一般以以下的形式出现： ns1.domain.com、ns2.domain.com等。 简单的说，NS记录是指定由哪个DNS服务器解析你的域名。

### TTL

TTL是DNS记录中的一个字段，表示特定记录的有效期。它定义了记录在DNS缓存中存储的时间，通常以秒为单位。当DNS解析器查询域名时，它将获取与之关联的TTL值，然后在TTL值到期之前重用缓存的DNS记录。一旦TTL过期，解析器将重新查询DNS服务器以获取最新的记录。TTL的存在有助于减轻DNS服务器的负载，同时确保DNS记录在需要时及时更新。
