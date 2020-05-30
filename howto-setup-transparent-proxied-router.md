如何在路由器中实现透明代理？
===

0 互联网现状
---


目前整个互联网环境，被破坏最严重地部分，是 Web 服务体验。当直接破坏难以实现时，就会从流程链的上下游着手，如：DNS 污染。

其它地互联网服务类型，例如：邮件，可能小部分会受到 Web 服务上下游破坏地余震，但整体上基本不受影响。

Web 服务的提供方式有三种：

* HTTP - 国内主流
* HTTPS - 国外主流
* SPDY - 试验阶段

HTTP 方式数据公开，因此最容易被破坏。

HTTPS 方式数据全程加密，中间人攻击很难达成，因此 DNS 污染 和 IP 封锁 较多。

SPDY 方式目前可能因为关注不多，所以无破坏。

1 透明代理技术选型
---

### 1.1 基本架构

透明转发操作可以直接交由 iptables 完成，`REDIRECT` 操作是其内核自带地。

代理服务选择 [shadowsocks-libev][] ，当前的 v1.4 版本已经实现了对 iptables `REDIRECT` 支持。

[shadowsocks-libev]: https://github.com/madeye/shadowsocks-libev

DNS 服务选择 dnsmasq 完成。

### 1.2 效率优化

转发调度操作选择 iptables geoip 模块，使访问国内 Web 服务时直连，绕过代理。

代理调度服务选择 [privoxy](http://www.privoxy.org) ，但其作为前置透明代理时，一样有着不支持 HTTPS 地通病。

DNS 可靠性验证选择 iptables u32 模块，初步防御。

### 1.3 弃用 GFWList

该列表太大了！诸多条目可能是我今生都不会访问地…何必非要强迫路由吃下？

花五分钟大概了解一下各种配置格式，然后针对性地配置即可。

2 配置 HTTP 透明代理
---

本节与下一节中，所有待自行设定地项，统一写作 `<NAME>` 格式。请注意调整。

### 2.1 配置 shadowsocks

使用 `/usr/bin/ss-local` 作为 socks5 代理服务器程序，远端端口勿必使用 1080 、 3128 、 8080 这种代理服务典型端口。

其余各种不提。

### 2.2 配置 privoxy

主配置 `/etc/privoxy/config` 中增加一条 `actionsfile freedom.action` 指令，文件名随意。

写入以下内容到上述指令对应地文件中：

```
{+forward-override{forward-socks5 127.0.0.1:<SS-LOCAL-PORT>  .} \
}
```

**注意：*\<SS-LOCAL-PORT>* 是 `/usr/bin/ss-local` 本地端口。**

### 2.3 配置 iptables

[准备 geoip 数据库](http://www.howtoforge.com/xtables-addons-on-centos-6-and-iptables-geoip-filtering)后，在终端执行：

```
iptables -t nat -N freedom
iptables -t nat -A freedom -d <SS-LOCAL-SERVER> -j RETURN
iptables -t nat -A freedom -d <NAT-NET> -j RETURN
iptables -t nat -A freedom -d 127/8 -j RETURN
iptables -t nat -A freedom -m geoip --dst-cc CN -j RETURN
iptables -t nat -A freedom -p tcp --dport 80 -j REDIRECT --to-ports <PRIVOXY-PORT>

iptables -t nat -I PREROUTING -p tcp -m multiport --dports 80,443 -j freedom

iptables -t mangle -N freedom
iptables -t mangle -A freedom -m u32 --u32 "0x0&0xf000000=0x5000000&&0x16&0xffff@0x10=0xd8ddbcb6,0xd8eab30d,0xf3b9bb27,0x4a7d7f66,0x4a7d9b66,0x4a7d2771,0x4a7d2766,0xd155e58a" -j DROP
iptables -t mangle -A freedom -m u32 --u32 "0x0&0xf000000=0x5000000&&0x16&0xffff@0x10=0xcab50755,0xcb620741,0xcba1e6ab,0xcf0c5862,0xd0381f2b,0xd1244921,0xd1913632,0xd1dc1eae,0xd35e4293,0xd5a9fb23" -j DROP
iptables -t mangle -A freedom -m u32 --u32 "0x0&0xf000000=0x5000000&&0x16&0xffff@0x10=0x422dfced,0x480ecd63,0x480ecd68,0x4e10310f,0x5d2e0859,0x80797e8b,0x9f6a794b,0xa9840d67,0xc043c606,0xca6a0102" -j DROP
iptables -t mangle -A freedom -m u32 --u32 "0x0&0xf000000=0x5000000&&0x16&0xffff@0x10=0x42442b2,0x807c62d,0x253d369e,0x2e52ae44,0x3b1803ad,0x402158a1,0x4021632f,0x4042a3fb,0x4168cafc,0x41a0db71" -j DROP

iptables -t mangle -A PREROUTING -p udp --sport 53 -j freedom
```

**注意：*\<SS-LOCAL-SERVER>* 是远端 shadowsocks 服务器 IP。**

**注意：*\<NAT-NET>* 是本地局域网网段，如：`192.168.1/24`。**

**注意：*\<PRIVOXY-PORT>* 是 privoxy 端口。**

3 配置 HTTPS 透明代理
---

### 3.1 配置 shadowsocks

使用 `/usr/bin/ss-redir` 作为 iptables `REDIRECT` 代理服务器程序。

### 3.2 配置 iptables

在终端执行：

```
iptables -t nat -N freedom-https
iptables -t nat -A freedom-https -j ACCEPT

iptables -t nat -A freedom -j freedom-https
iptables -t nat -A freedom -p tcp -j REDIRECT --to-ports <SS-REDIR-PORT>
```

**注意：*\<SS-REDIR-PORT>* 是 `/usr/bin/ss-redir` 本地端口。**

4 修复破坏点
---

以 [Youtube](http://www.youtube.com) 为例，其同时提供了 HTTP 和 HTTPS 两种方式地服务。页面可以基于 HTTP 方式打开，但视频就只能基于 HTTPS 方式。

### 4.1 HTTP 方式时使用代理

在 `/etc/privoxy/freedom.action` 配置文件尾部追加一行：

```
.youtube.com
```

重启 privoxy。

### 4.2 修复 DNS 污染

如果依旧无法访问，则在 `/etc/dnsmasq.conf` 配置文件尾部追加一行：

```
server=/youtube.com/218.102.23.228
```

重启 dnsmasq。

**注意：`218.102.23.228` 是香港网上行电信服务商提供地 DNS 服务器地址，您也可以更换成自己更习惯地真实 DNS 。**

### 4.3 HTTPS 方式时使用代理

查询域名对应地 IP 地址后，在终端执行：

```
iptables -t nat -I freedom-https -d <SERVICE-IP> -j RETURN
```

**注意：*\<SERVICE-IP>* 是相应服务的 IP 地址或网段。**

5 测量与继续优化
---

选择使用 iptables 、 dnsmasq 、 privoxy 和 [shadowsocks-libev][] 最主要地原因，是绝大多数 Linux 发行版都可以通过包管理快速安装，其中也包括了 [OpenWRT][]。 

[OpenWRT]: https://openwrt.org

但实际使用时，会发现在访问国外服务时，总是有点慢…一来是因为国外服务的 DNS TTL 都设得很低，二来是因为无论有没有需要，其实都是通过 privoxy 了地。

怎么破？

### 5.1 网关服务器

如果是拿单独一台机器作网关来扮演路由地角色，那么利用好大内存，可以：

1. dnsmasq + pdnsd

    使用 pdnsd 地本地 DNS 缓存机制，可以强制改变 DNS 记录的 TTL ，进一步减少 DNS 重询次数。
    
    保留 dnsmasq ，则是因为还得靠它来提供 DHCP 服务。

2. privoxy -> squid

    使用 squid 地页面缓存机制，同样是强制改变页面缓存的时间，降低对真实服务地访问频次。

### 5.2 OpenWRT

目前基于路由器的自制内嵌系统，活得还算可以地，貌似也就 OpenWRT 一家了。所以暂时就只关注这个。

路由器的内存如何合理利用？几乎是一个永恒地难题。基础就那么一丁点，怎么都难以玩出花来。所以：

1. dnsmasq + pdnsd

    仍然需要使用 pdnsd ，主要原因是针对被修复地国外服务，对其 DNS 地查询也是在境外完成地，速度慢再所难免。而搭上 dnsmasq 这么一太实诚的队友，就有点不好地感觉了。

1. privoxy ->

    放弃费力不讨好的 privoxy 吧！跑一个小时， privoxy 能吃到 40M+ 内存，让人怎么活？
    
    **警告：此项操作会直接导致一些公共服务平台无法访问，诸如 `.blogspot.com` 、 `.wordpress.com` 等等。这是一个艰难地抉择！**
    
2. `/usr/bin/ss-local` ->

    舍弃与 privoxy 配合地 shadowsocks socks5 服务，直接将需要地请求全部转给 `/usr/bin/ss-redir` 处理。

这时， iptables nat 表 freedom 链就得动一下小手术了（参见 2.3 和 3.2 小节）。调整之后地命令如下：

```
iptables -t nat -N freedom
iptables -t nat -A freedom -d <SS-LOCAL-SERVER> -j RETURN
iptables -t nat -A freedom -d <NAT-NET> -j RETURN
iptables -t nat -A freedom -d 127/8 -j RETURN
iptables -t nat -A freedom -m geoip --dst-cc CN -j RETURN
iptables -t nat -A freedom -j freedom-https
iptables -t nat -A freedom -p tcp -j REDIRECT --to-ports <SS-REDIR-PORT>
```

对所有非 shadowsocks 服务器、非局域网、非本机、非国内的地址，统统进行检查。只要不是在标记列表内，直连。

A 参考文献
---

1. [《OPENWRT + tomato 透明代理+DNS清理》](https://gist.github.com/wen-long/9635831)，作者 [@wen-long](https://gist.github.com/wen-long)，最后修订于 2014 年 3 月 24 日。

B 修订记录
---

* 2014-07-29 调整 [5.2 OpenWRT](#52-openwrt)。
* 2014-07-28 增加 [5 测量与继续优化](#5-测量与继续优化)。
