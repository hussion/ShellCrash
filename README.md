<a target="_blank" href="https://github.com/juewuy/ShellCrash/releases">
  <img src="https://img.shields.io/github/release/juewuy/ShellCrash.svg?style=flat-square&label=ShellCrash&colorB=green">
</a>

[中文](README_CN.md)

ShellClash说明文档

目录结构
·安装目录
默认安装目录为/etc/clash或/data/clash等

可手动指定任意目录安装，安装完成后可以使用【echo $clashdir】命令查询安装目录

目录包含以下文件：

~clash：clash核心文件

~clash.sh/start.sh/getdate.sh：ShellClash运行脚本文件

~Country.mmdb：Geoip数据库文件

~config.yaml：clash基础配置文件

~config.yaml.bak：clash配置文件备份

~mark：脚本运行配置文件

~mac：脚本mac过滤功能配置文件

~/ui/*：本地dashboard网页文件及PAC文件

·服务文件
OpenWrt的服务文件为/etc/init.d/clash

Debian/Centos/Armbian等标准Linux系统的服务文件在/etc/systemd/system或者/usr/lib/systemd/system/下，名为clash.service

功能说明
1 启动/重启clash服务
2 clash功能设置：
​ 1 切换clash运行模式：支持切换多种运行模式，主要涉及iptables或nftables的不同配置

​ 2 切换DNS运行模式：支持切换fake-ip或者真实ip的dns模式

​ 3 跳过本地证书验证：当节点出现证书验证错误时使用此选项可以使节点正常使用

​ 4 只代理常用端口：只代理22,53,587,465,995,993,143,80,443等常用端口，主要用于屏蔽p2p流量

​ 5 过滤局域网mac地址：使用黑名单或白名单方式依照局域网设备的网卡mac地址进行过滤，被过滤的设备不会走clash的dns以及透明路由

​ 6 设置本机代理服务：使用环境变量或者iptables/nftables对本机发出的流量进行路由，路由设备通常无需开启

​ 7 屏蔽QUIC流量：使用iptables或者nftables，对443端口的udp请求进行reject，由于改善YouTube访问速度，如果你需要使用ChatGPT，建议不要开启

​ 8 绕过CN-IP（Redir-Host模式）：使所有在CNIP列表内的地址不走clash内核的透明路由，以提升对应地址的访问速度

​ 8 管理Fake-ip过滤列表：用以自定义额外的Fake-ip-filter域名，防止部分地址因fake-ip导致无法访问

3 停止clash服务：
停止clash服务并且停止相关的一切路由、防火墙以及本机代理规则

4 clash启动设置：
​ 1 允许/禁止clash开机启动：禁止或者启用clash的开机启动服务

​ 2 使用保守模式：不使用OpenWrt的procd或者Linux的Systemd服务进行启动，改为使用linux系统通用的nohup &方式启动并配合crond服务进行进程守护

​ 3 设置自启延时：首次开机启动时，延迟若干秒进行启动，用于解决部分设备直接启动时无法正确启动或者无法正确配置透明路由的问题

​ 4 启用小闪存模式：将体积较大的内核文件、GeoIP数据库文件等放在内存或者自定义的外置存储目录中，减少闪存占用

5 设置定时任务
使用系统自带的crontab功能，智能配置与clash相关的定时任务，支持配置定时启动、重启、关闭clash功能，支持配置定时更新订阅功能。

6 导入节点/订阅链接
使用在线的sub服务，快速导入ss/ssr/vmess/trojan/vless/hysteria等节点链接，并生成在线配置文件下载到本地作为clash的配置文件

7 clash进阶设置
​ 1 ipv6相关：对ipv6进行支持的相关配置

​ 3 配置公网及局域网防火墙：脚本默认屏蔽了面板及http代理端口从公网的访问流量，可以通过此处进行开启

​ 4 启用域名嗅探：Meta专属功能，通过读取ip链接中的域名信息，对域名进行还原，可以优化TV平台视频软件的连接效果

​ 5 启用节点绕过：对本地配置文件中的节点域名或IP自动配置直连规则，用于防止在终端设备同时开启clash等软件时产生多重流量

​ 6 配置内置DNS服务：对clash的内置DNS进行额外配置

​ 7 自定义配置：支持通过本地文件覆写相关的clash配置

​ 8 手动指定相关端口、秘钥：类似自定义配置功能，可以手动对配置中的相关端口秘钥等数据进行自定义

​ 9 重置/备份/还原脚本设置

8 其他工具
​ 1 测试菜单：一些用于debug或者测试clash运行的快捷命令

​ 2 新手引导：用于重新进入新手引导

​ 3 日志及推送工具：用于查看ShellClash脚本的运行日志，或者配置日志推送通道将相关日志推送到Telegram等软件

​ 5 小米系统自动更新：用于禁止小米路由系统的自动更新

​ 6 小米设备软固化SSH：用于小米路由官方系统通过脚本内置软件在开机启动时自动打开SSH服务

​ 7 配置DDNS服务(限OpenWrt)：下载额外的脚本，可以打开OpenWrt定制系统更多的DDNS设置

​ 8 小米设备Tun模块修复：由于部分小米路由设备，修复因刷机等导致的Tun模块丢失问题

9 更新/卸载
​ 1 更新管理脚本：在线更新管理脚本

​ 2 切换clash核心：在线更新/切换clash核心

​ 3 更新GeoIP数据库：在线更新GeoIP数据库文件

​ 4 安装本地Dashboard面板：安装一个基于clash内置web服务的本地面板

​ 5 安装更新本地根证书文件：用于解决部分设备出现SSL证书验证失败的问题

​ 6 查看本地PAC文件：用户部分设备快捷配置本地http代理

​ 7 切换安装源及安装版本：内置了多个不同安装源以及安装版本用以切换，也包括版本回退

​ 9 卸载：完全移除所有ShellClash的相关文件和相关环境变量，该操作不可逆

快捷命令
	clash -t #测试模式
	clash -h #帮助列表
	clash -u #卸载脚本
	clash -s start #启动/重启服务
	clash -s stop #停止服务
	clash -s updateyaml #更新配置文件
	安装目录/start.sh init #开机初始化
	#在线求助：t.me/ShellClash
	#官方博客：juewuy.github.io
	#发布页面：github.com/juewuy/ShellClash




