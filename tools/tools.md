如何一行命令自建一个IPSec/L2TP的VPN？首先，找一台国外的VPS，装个最新版的Ubuntu/CentOS，
然后执行：docker run -d -p 500:500/udp -p 4500:4500/udp -p 1701:1701/tcp -e PSK=共享密码 -e USERNAME=用户名 -e PASSWORD=密码 siomiz/softethervpn 