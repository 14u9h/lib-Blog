---
layout: post
title: Nmap使用文档翻译
categories: 神兵利器
description: Nmap使用文档翻译
keywords: Nmap,Nmap使用文档
---

### Nmap 7.12SVN ( https://nmap.org )

#### 命令格式: nmap [Scan Type(s)] [Options] {target specification}

#### TARGET SPECIFICATION:
* nmap可以扫描主机名,ip,网段等表示方式.
* 例如: scanme.nmap.org,  microsoft.com/24,  192.168.0.1， 10.0.0-255.1-254
 *  -iL 文件路径: 从文件中批量读取待检测的主机名,ip,网段
 *  -iR <num hosts>: 随机选取,进行扫描.如果-iR指定为0,则是无休止的扫描
 *  --exclude 主机1[,主机2][,主机3],...: 批量扫描任务中需要排除的主机
 *  --excludefile 文件路径: 从文件中批量读取需排除的主机

#### 主机发现:
* -sL: List Scan - 列表扫描，仅将指定的目标的IP列举出来，不进行主机发现
* -sn: Ping Scan - Ping扫描，不进行端口扫描
* -Pn: 把所有的主机都当做在线 -- 跳过主机发现这一步
* -PS/PA/PU/PY[portlist]: 使用TCPSYN/ACK或SCTP INIT/ECHO方式进行发现
* -PE/PP/PM: 使用ICMP echo, timestamp and netmask 请求包发现主机
* -PO[protocol list]: 使用IP协议包探测对方主机是否开启
* -n/-R: -n表示不进行DNS解析；-R表示总是进行DNS解析 （默认为：有时）
* --dns-servers <serv1[,serv2],...>: 指定DNS服务器
* --system-dns: Use OS's DNS resolver
* --traceroute: 追踪每个路由节点

#### :扫描技术
* -sS/sT/sA/sW/sM: TCP SYN扫描/TCP connect()扫描/TCP ACK扫描/TCP窗口扫描/TCP Maimon扫描
* -sU: UDP 扫描
* -sN/sF/sX:TCP Null /TCP FIN /TCP Xmas扫描
* --scanflags <flags>: 定制的TCP扫描
* -sI <zombie host[:probeport]>: Idle scan //僵尸主机扫描
* -sY/sZ: SCTP INIT/COOKIE-ECHO scans
* -sO: IP协议扫描
* -b <FTP跳板主机>: FTP弹跳扫描

#### 端口说明与扫描顺序:
* -p <端口范围>: 只扫描指定的端口
    例如: -p22; -p1-65535; -p U:53,111,137,T:21-25,80,139,8080,S:9
* --exclude-ports <端口范围>: 过滤掉不需要扫描的端口
* -F: 快速模式 - 只扫描常见的端口
* -r: 按端口数值大小顺序扫描，常见端口不优先扫描
* --top-ports <number>: Scan <number> most common ports
* --port-ratio <ratio>: Scan ports more common than <ratio>

#### 服务和版本检测:
* -sV: 探测开放的端口以确定开放出来的服务或版本信息
* --version-intensity <数值>: 设置扫描强度1-9
* --version-light: 轻量级扫描，只扫两个探测报文 (intensity 2)
* --version-all: 尝试所有探测报文 (intensity 9)
* --version-trace: 显示扫描的详细信息 (用于调试)

#### 脚本扫描:
* -sC: equivalent to --script=default
* --script=<Lua scripts>: <Lua scripts> is a comma separated list of
           directories, script-files or script-categories
* --script-args=<n1=v1,[n2=v2,...]>: provide arguments to scripts
* --script-args-file=filename: provide NSE script args in a file
* --script-trace: Show all data sent and received
* --script-updatedb: Update the script database.
* --script-help=<Lua scripts>: Show help about scripts.
           <Lua scripts> is a comma-separated list of script-files or
           script-categories.

#### 操作系统检测:
* -O: 启用操作系统检测
* --osscan-limit: Limit OS detection to promising targets
* --osscan-guess: 当检测不出操作系统版本时使用这个进行相似度匹配
* --fuzzy:相似度匹配+2

#### 时间和性能:
* Options which take <time> are in seconds, or append 'ms' (milliseconds),
* 's' (seconds/秒), 'm' (minutes/分钟), or 'h' (hours/小时) to the value (e.g. 30m).
* -T<0-5>: Set timing template (higher is faster)
* --min-hostgroup/max-hostgroup <size>: Parallel host scan group sizes
* --min-parallelism/max-parallelism <numprobes>: Probe parallelization
* --min-rtt-timeout/max-rtt-timeout/initial-rtt-timeout <time>: Specifies
      probe round trip time.
* --max-retries <tries>: Caps number of port scan probe retransmissions.
* --host-timeout <time>: Give up on target after this long
* --scan-delay/--max-scan-delay <time>: Adjust delay between probes
* --min-rate <number>: Send packets no slower than <number> per second
* --max-rate <number>: Send packets no faster than <number> per second

#### 防火墙/IDS躲避和欺骗:
* -f; --mtu <val>: fragment packets (optionally w/given MTU)
* -D <decoy1,decoy2[,ME],...>: Cloak a scan with decoys
* -S <IP_Address>: Spoof source address
* -e <iface>: Use specified interface
* -g/--source-port <portnum>: Use given port number
* --proxies <url1,[url2],...>: Relay connections through HTTP/SOCKS4 proxies
* --data <hex string>: Append a custom payload to sent packets
* --data-string <string>: Append a custom ASCII string to sent packets
* --data-length <num>: Append random data to sent packetsTCP
* --ip-options <options>: Send packets with specified ip options
* --ttl <val>: Set IP time-to-live field
* --spoof-mac <mac address/prefix/vendor name>: Spoof your MAC address
* --badsum: Send packets with a bogus TCP/UDP/SCTP checksum

#### 输出:
* -oN/-oX/-oS/-oG <file>: Output scan in normal, XML, s|<rIpt kIddi3,
     and Grepable format, respectively, to the given filename.
* -oA <basename>: Output in the three major formats at once
* -v: Increase verbosity level (use -vv or more for greater effect)
* -d: Increase debugging level (use -dd or more for greater effect)
* --reason: Display the reason a port is in a particular state
* --open: Only show open (or possibly open) ports
* --packet-trace: Show all packets sent and received
* --iflist: Print host interfaces and routes (for debugging)
* --append-output: Append to rather than clobber specified output files
* --resume <filename>: Resume an aborted scan
* --stylesheet <path/URL>: XSL stylesheet to transform XML output to HTML
* --webxml: Reference stylesheet from Nmap.Org for more portable XML
* --no-stylesheet: Prevent associating of XSL stylesheet w/XML output

#### 其他:
* -6: Enable IPv6 scanning
* -A: Enable OS detection, version detection, script scanning, and traceroute
* --datadir <dirname>: Specify custom Nmap data file location
* --send-eth/--send-ip: Send using raw ethernet frames or IP packets
* --privileged: Assume that the user is fully privileged
* --unprivileged: Assume the user lacks raw socket privileges
* -V: Print version number
* -h: Print this help summary page.

#### 实例:
* nmap -v -A scanme.nmap.org
* nmap -v -sn 192.168.0.0/16 10.0.0.0/8
* nmap -v -iR 10000 -Pn -p 80
SEE THE MAN PAGE (https://nmap.org/book/man.html) FOR MORE OPTIONS AND EXAMPLES
