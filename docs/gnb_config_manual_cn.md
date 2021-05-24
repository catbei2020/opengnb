GNB Linux 部署说明

[GNB](https://github.com/gnbdev/gnb "GNB")是一个开源的去中心化的具有极致内网穿透能力的通过P2P进行三层网络交换的虚拟组网系统。


## gnb的命令行参数

执行`gnb -h`可以看到gnb在当前平台所支持的参数，这里只对一些已经明确固定下来的参数进行解释


|参数|明细|
|-|-|
|-c, --conf|指定gnb node的目录|
|-i, --ifname|指定虚拟网卡的的名字，这在macOS和windows上是无效的，这些系统对虚拟网卡的命名有自己的规则|
|-4, --ipv4-only|禁用ipv6，gnb将不通过ipv6地址收发数据，gnb开启的虚拟网卡不会绑定ipv6地址，由于禁用了ipv6，因此gnb可以设置小于1280的mtu,对于一些限制比较多的网络环境可以利用这个特性尝试使用更小的mtu|
|-6, --ipv6-only|禁用ipv4，gnb将不通过ipv4地址收发数据，gnb开启的虚拟网卡不会绑定ipv4地址|
|-d, --daemon|作为daemon进程启动，Windows不支持这个选项|
|-q, --quiet|禁止在控制台输出信息|
|-l, --listen|listen address default is '0.0.0.0:9001'|
|--log-file-path|指定输出文件日志的路径，如果不指定将不会产生日志文件|
|--log-console-level|log-console-level 0-3|
|--log-file-level|log-file-level    0-3|
|--log-udp-level|log-udp-level     0-3|
|--core-log-level|core-log-level    0-3|
|--pf-log-level|pf-log-level      0-3|
|--main-log-level|main-log-level    0-3|
|--node-log-level|node-log-level    0-3|
|--index-log-level|index-log-level   0-3|
|--detect-log-level|detect-log-level  0-3|
|--node-woker-queue-length|node  woker queue length|
|--index-woker-queue-length|index woker queue length|
|--port-detect-start|port detect start|
|--port-detect-end|port detect end|
|--port-detect-range|port detect range|
|--mtu|虚拟网卡的mtu，在比较糟糕的网络环境下ipv4可以设为532,ipv6不可小于1280|
|--crypto|'xor' or 'rc4' or 'none' default is 'xor'; 设定gnb传输数据的加密算法，选择'none'就是不加密，默认是xor使得在CPU运算能力很弱的硬件上也可以有较高的数据吞吐能力。未来会支持aes算法。两个gnb节点必须保持相同的加密算法才可以正常通讯。|
|--crypto-key-update-interval|'hour' or 'minute' or none default is 'none';gnb的节点之间可以通过时钟同步变更密钥，这依赖与节点的时钟必须保持较精确的同步，由于考虑到实际环境中一些节点时钟可能2无法及时同步时间，因此这个选项默认是不启用，如果运行gnb的节点能够保证同步时钟，可以考虑选择一个同步更新密钥的间隔，这可以提升一点通讯的安全性。|
|--multi-index-type|'simple-fault-tolerant' or 'simple-load-balance' default is 'simple-fault-tolerant';如果设置了多个index节点，那么可以选择一个选取index节点的方式，负载均衡或容错模式，这个选项目前还不完善，容错模式只能在交换了通讯密钥的节点之间进行|
|--multi-forward-type|'simple-fault-tolerant' or 'simple-load-balance' default is 'simple-fault-tolerant';如果有多个forward节点，可以选择一个forward节点的方式，负载均衡或在容错模式|
|--socket-if-name|example: 'eth0', 'eno1', only for unix-like os;在unix-like系统上可以让gnb的数据通过指定物理网卡发送，这里需要用户输入物理网卡的名字，Windows不支持这个特性，也看不到该选项|
|--address-secure|'hide part of ip address in logs 'on' or 'off' default is 'on'|
|--if-dump|'dump the interface data frame 'on' or 'off' default is 'off';把经过gnb开启的虚拟网卡的ip分组在日志中输出，这样方便调试系统|
|--enabled-multi-socket|开启多端口探测,在nat穿透端口探测过程中可以较大提升nat穿透成功率|
|--disabled-direct-forward|disabled direct forward|
|--disabled-index-worker|disabled index worker|
|--disabled-index-service|disabled index service|
|--disabled-tun|不启动虚拟网卡，仅作为gnb index服务启动，由于没有启动虚拟网卡，因此设了这个选项时不需要用root权限去启动gnb|
--disabled-fwdu0|disabled forward udp type 0|
|--pid-file|指定保存gnb进程id的文件，方便通过脚本去kill进程，如果不指定这个文件，pid文件将保存在当前节点的配置目录下|
|--node-cache-file|gnb会定期把成功连通的节点的ip地址和端口记录在一个缓存文件中，gnb进程在退出后，这些地址信息不会消失，重新启动进程时会读入这些数据，这样新启动gnb进程就可能不需通过index 节点查询曾经成功连接过的节点的地址信息|


## gnb_es的命令行参数

执行`gnb_es -h`可以看到gnb_es在当前平台所支持的参数
|参数|明细|
|-|-|
|-b, --ctl_block|ctl block mapper file|
|-s, --service|service mode|
|-d, --daemon|daemon|
|--upnp|upnp|
|--resolv|resolv|
|--dump-address|dump address|
|--broadcast-addres|broadcast addre|
|--pid-file|pid file|
|--wan-address6-file|wan address6 file|
|--if-up|call at interface up|
|--if-down|call at interface down|
|--log-udp4|send log to the address ipv4 default is '127.0.0.1:9000'|
|--log-udp-type|the log udp type 'binary' or 'text' default is 'binary'|


