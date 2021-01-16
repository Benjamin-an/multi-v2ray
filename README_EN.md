# multi-v2ray
a tool to manage v2ray/xray config json, support multiple user && group manage  
![](https://img.shields.io/pypi/v/v2ray-util.svg) 
[![Downloads](https://pepy.tech/badge/v2ray-util)](https://pepy.tech/project/v2ray-util)
[![Downloads](https://pepy.tech/badge/v2ray-util/month)](https://pepy.tech/project/v2ray-util)
![](https://img.shields.io/docker/pulls/jrohy/v2ray.svg)
![](https://img.shields.io/github/license/Jrohy/multi-v2ray.svg)

## [中文](README.md)  [English](README_EN.md)

## Feature
- Support Xray manage, different commands (v2ray/xray) enter different core management
- V2ray && Iptables Traffic Statistics
- Command line to manage
- Multiple user && port manage
- Cloudcflare cdn mode
- Support pure ipv6 VPS
- Support Docker
- Dynamic port
- Ban bittorrent
- Range port
- TcpFastOpen
- Vmess/Socks5/MTproto share link
- Support protocol modify:
  - TCP
  - Fake http
  - WebSocket
  - mkcp
  - mKCP + srtp
  - mKCP + utp
  - mKCP + wechat-video
  - mKCP + dtls
  - mKCP + wireguard
  - HTTP/2
  - Socks5
  - MTProto
  - Shadowsocks
  - Quic
  - VLESS
  - VLESS_WS
  - VLESS_XTLS
  - Trojan

## How To Use
Oracle-ubuntu
```
apt-get update -y && apt-get install curl -y
```
new install
```
source <(curl -sL https://multi.netlify.app/v2ray.sh)
```

keep profile to update
```
source <(curl -sL https://multi.netlify.app/v2ray.sh) -k
```

uninstall
```
source <(curl -sL https://multi.netlify.app/v2ray.sh) --remove
```
bbr
```
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh"
chmod +x tcp.sh
./tcp.sh
```
Certificate application failed solution
```
一、oracle甲骨文云必要操作
进入ROOT模式：sudo -i

1：安装相关依赖
centos系统下
yum update -y                                                                                                
apt-get update -y && apt-get install curl -y

ubuntu系统下
apt update -y
apt-get update -y && apt-get install curl -y

2：删除、关闭、打开各自系统的无用附件、防火墙、端口及规则
注意Centos系统下：
删除多余附件
systemctl stop oracle-cloud-agent
systemctl disable oracle-cloud-agent
systemctl stop oracle-cloud-agent-updater
systemctl disable oracle-cloud-agent-updater

停止firewall
systemctl stop firewalld.service
禁止firewall开机启动
systemctl disable firewalld.service

注意Ubuntu系统下：
开放所有端口
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -F

Ubuntu镜像默认设置了Iptable规则，关闭它
apt-get purge netfilter-persistent
reboot
或者强制删除
rm -rf /etc/iptables && reboot
```
## Command Line
```bash
v2ray/xray [-h|help] [options]
    -h, help             get help
    -v, version          get version
    start                start V2Ray
    stop                 stop V2Ray
    restart              restart V2Ray
    status               check V2Ray status
    new                  create new json profile
    update               update v2ray to latest
    update [version]     update v2ray to special version
    update.sh            update multi-v2ray to latest
    add                  add new group
    add [protocol]       create special protocol, random new port
    del                  delete port group
    info                 check v2ray profile
    port                 modify port
    tls                  modify tls
    tfo                  modify tcpFastOpen
    stream               modify protocol
    cdn                  cdn mode
    stats                v2ray traffic statistics
    iptables             iptables traffic statistics
    clean                clean v2ray log
    log                  check v2ray log
    rm                   uninstall core
```

## Docker Run
default will create random port + random header(srtp | wechat-video | utp | dtls) kcp profile(**if use xray replace image to jrohy/xray**)  
```
docker run -d --name v2ray --privileged --restart always --network host jrohy/v2ray
```

custom v2ray config.json:
```
docker run -d --name v2ray --privileged -v /path/config.json:/etc/v2ray/config.json --restart always --network host jrohy/v2ray
```

check v2ray profile:
```
docker exec v2ray bash -c "v2ray info"
```

**warning**: if u run with centos, u should close firewall first
```
systemctl stop firewalld.service
systemctl disable firewalld.service
```

## Dependent
v2ray docker: https://hub.docker.com/r/jrohy/v2ray  
xray docker: https://hub.docker.com/r/jrohy/xray
pip: https://pypi.org/project/v2ray-util/  
python3: https://github.com/Jrohy/python3-install  
acme: https://github.com/Neilpang/acme.sh
