t_proxy_FTP.c为源码，tproxyFTP为可执行程序。

首先开启防火墙数据转发功能：echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward；其次使用Netfilter将防火墙接收到的TCP数据包全部转发到8888端口：sudo iptables -t nat -A PREROUTING -p tcp -j REDIRECT --to-ports 8888；编译t_proxy_FTP.c：gcc -o tproxyFTP t_proxy_FTP.c -lpthread；运行编译后的可执行程序，使其监听端口8888：./tproxyFTP -p 8888。防火墙开始运行。