# multi-v2ray
V2ray/Xray多用户管理脚本，向导式管理[新增|删除|修改]传输协议  
![](https://img.shields.io/pypi/v/v2ray-util.svg) 
[![Downloads](https://pepy.tech/badge/v2ray-util)](https://pepy.tech/project/v2ray-util)
[![Downloads](https://pepy.tech/badge/v2ray-util/month)](https://pepy.tech/project/v2ray-util)
![](https://img.shields.io/docker/pulls/jrohy/v2ray.svg)
![](https://img.shields.io/github/license/Jrohy/multi-v2ray.svg)

## [中文](README.md)  [English](README_EN.md)

## 特色
- [x] 支持Xray管理, v2ray和xray相互独立, 不同命令(v2ray/xray)进入不同的core管理
- [x] 调用v2ray官方api进行流量统计
- [x] **多用户, 多端口管理**, 混合传输协议管理不再是梦
- [x] 首次安装时产生随机端口，默认配置mkcp + 随机一种 (srtp | wechat-video | utp | dtls | wireguard) header伪装;  
  安装完成显示配置信息;
- [x] 查看配置信息显示vmess字符串(v2rayN的分享链接格式)
- [x] 生成**Telegram**的socks5/MTProto分享链接, 支持socks5 + tls组合
- [x] 支持http/2, 随机生成伪装h2 path
- [x] 开启关闭tcpFastOpen
- [x] 直接开启[CDN](https://github.com/Jrohy/multi-v2ray/wiki/CloudFlare-cdn%E4%BB%A3%E7%90%86v2ray%E6%B5%81%E9%87%8F)
- [x] 开启关闭动态端口
- [x] 定时更新v2ray(需手动开启)
- [x] 支持新版v2ray配置文件格式(v4.1+)
- [x] 支持范围端口修改
- [x] 支持程序和**命令行参数**管理控制
- [x] 支持docker部署
- [x] 支持VLESS和Trojan以及XTLS(v4.31.0+)
- [x] 支持纯ipv6 vps
- [x] 禁止BT

## 功能
- 一键 启动 / 停止 / 重启 V2ray 服务端
- 流量统计(v2ray && iptables)
- 命令行模式管理v2ray
- 支持多用户， 多端口管理
- 开启关闭动态端口
- bittorrent的禁止与放行
- 单端口, 范围端口的修改
- 直接走Cloudcflare cdn
- 开启关闭tcpFastOpen
- 快速查看服务器连接信息, 常规配置修改
- 自由更改**传输配置**：
  - 常规TCP
  - HTTP头部伪装
  - WebSocket流量
  - 常规mKCP流量
  - mKCP 伪装 FaceTime通话流量(srtp)
  - mKCP 伪装 BT下载流量(utp)
  - mKCP 伪装 微信视频通话流量(wechat-video)
  - mKCP 伪装 DTLS 1.2流量(dtls)
  - mKCP 伪装 WireGuard流量(wireguard)
  - HTTP/2的tls流量(h2)(需备域名) 
  - Socks5
  - MTProto
  - Shadowsocks
  - Quic
  - VLESS
  - VLESS_WS
  - VLESS_XTLS
  - Trojan

## Oracle-安装Curl命令
```
 apt-get update -y && apt-get install curl -y
```
## 安装命令
```
source <(curl -sL https://multi.netlify.app/v2ray.sh) --zh
```

## 升级命令(保留配置文件更新)
```
source <(curl -sL https://multi.netlify.app/v2ray.sh) -k
```

## 卸载命令
```
source <(curl -sL https://multi.netlify.app/v2ray.sh) --remove
```
## bbr命令
```
wget -N --no-check-certificate "https://raw.githubusercontent.com/chiakge/Linux-NetSpeed/master/tcp.sh"
chmod +x tcp.sh
./tcp.sh
```
## 卸载v2ray脚本命令
```
bash <(curl -L -s https://multi.netlify.app/go.sh) --remove >/dev/null
```
## 卸载xray脚本命令
```
bash <(curl -L -s https://multi.netlify.app/go.sh) --remove -x >/dev/null
```
## 证书失败操作命令
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
## Euserv安装
```
一、VPS设置IPV4访问
因为德国小鸡是纯IPV6地址的，为了能访问Github下载文件所以要设置VPS能访问IPV4地址

  echo -e "nameserver 2001:67c:2b0::4•\nnameserver 2001:67c:2b0::6" > /etc/resolv.conf
二、基本插件安装
1、安装基本插件和curl

  apt-get update -y && apt-get install curl -y
三、证书安装
Euserv最难的就是获取证书，大部分脚本也是在这里错误，我们先运行下面的命令，自动安装时候证书错误再运行一次这个命令，重新安装自动安装xray命令就可以了

 bash /root/.acme.sh/acme.sh --issue -d 域名 --debug --standalone --keylength ec-256 --listen-v6
如果还有错误尝试一下下面的命令

 yum install socat #通过80端口生成证书的依赖 #centos7系统
 yum install netcat #centos7系统
 ​
 apt-get install openssl cron socat curl   #debian系统
 apt-get -y install netcat   #debian系统
 ​
 安装成功后执行 source ~/.bashrc 以确保脚本所设置的命令别名生效
四、一键安装代码
 bash <(curl -sL https://s.hijk.art/xray.sh)
Cloudflare的CDN，目前只能使用websocket协议，XTLS不支持websocket协议
```
## 命令行参数
```bash
v2ray/xray [-h|help] [options]
    -h, help             查看帮助
    -v, version          查看版本号
    start                启动 V2Ray
    stop                 停止 V2Ray
    restart              重启 V2Ray
    status               查看 V2Ray 运行状态
    new                  重建新的v2ray json配置文件
    update               更新 V2Ray 到最新Release版本
    update [version]     更新 V2Ray 到指定版本
    update.sh            更新 multi-v2ray 到最新版本
    add                  新增端口组
    add [protocol]       新增一种协议的组, 端口随机, 如 v2ray add utp 为新增utp协议
    del                  删除端口组
    info                 查看配置
    port                 修改端口
    tls                  修改tls
    tfo                  修改tcpFastOpen
    stream               修改传输协议
    cdn                  走cdn
    stats                v2ray流量统计
    iptables             iptables流量统计
    clean                清理日志
    log                  查看日志
    rm                   卸载core
```

## Docker运行

默认创建mkcp + 随机一种伪装头配置文件(**如果使用xray则换成镜像jrohy/xray**)：
```
docker run -d --name v2ray --privileged --restart always --network host jrohy/v2ray
```

自定义v2ray配置文件:
```
docker run -d --name v2ray --privileged -v /path/config.json:/etc/v2ray/config.json --restart always --network host jrohy/v2ray
```

查看v2ray配置:
```
docker exec v2ray bash -c "v2ray info"
```

**warning**: 如果用centos，需要先关闭防火墙
```
systemctl stop firewalld.service
systemctl disable firewalld.service
```

## 建议
安装完v2ray后强烈建议开启BBR等加速: [Linux-NetSpeed](https://github.com/chiakge/Linux-NetSpeed)  
使用Trojan和VLESS协议建议自行安装个nginx, 能让v2ray顺利Fallback到默认的80端口

## 依赖
v2ray docker: https://hub.docker.com/r/jrohy/v2ray  
xray docker: https://hub.docker.com/r/jrohy/xray  
pip: https://pypi.org/project/v2ray-util/  
python3: https://github.com/Jrohy/python3-install  
acme: https://github.com/Neilpang/acme.sh
