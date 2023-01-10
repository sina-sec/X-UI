# x-ui
[简体中文](./README.md) | ENGLISH 

XRAY panel that supports multi-protocol and multi-user
# Features

- System Status Monitoring
- Support multi-user and multi-protocol, web page visualization operation
- Supported protocols: vmess, vless, trojan, shadowsocks, dokodemo-door, socks, http
- Support for configuring more transport configurations
- Traffic statistics, limit traffic, limit expiration time
- Customizable xray configuration template
- Support https access panel (self-provided domain name + ssl certificate）
- Support one-click SSL certificate application and automatic renewal
- For more advanced configuration items, see Panel

# Install & Upgrade


Make sure your system `bash` and `curl` and `network` are ready,here we go

For Chinese users,please use the following command to install China supported version:  
```
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
```  
For English Users,please use the following command to install English supported version:  
```
bash <(curl -Ls https://raw.githubusercontent.com/sina-sec/x-ui/master/install_en.sh)
``` 
## Manual installation & upgrade

1. First download the latest compressed package from https://github.com/sina-sec/x-ui/releases, generally choose the `amd64` architecture
2. Then upload this compressed package to the `/root/` directory of the server, and use the `root` user to log in to the server

> If your server cpu architecture is not `amd64`, replace `amd64` in the command with other architectures

```
cd /root/
rm x-ui/ /usr/local/x-ui/ /usr/bin/x-ui -rf
tar zxvf x-ui-linux-amd64.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui
```

## Install using docker

> This docker tutorial and docker image are provided by [Chasing66](https://github.com/Chasing66)

1. install docker

```shell
curl -fsSL https://get.docker.com | sh
```

2. install x-ui

```shell
mkdir x-ui && cd x-ui
docker run -itd --network=host \
    -v $PWD/db/:/etc/x-ui/ \
    -v $PWD/cert/:/root/cert/ \
    --name x-ui --restart=unless-stopped \
    enwaiax/x-ui:latest
```

> Build your own image

```shell
docker build -t x-ui .
```

# common problem

## Migrating from v2-ui

First install the latest version of x-ui on the server where v2-ui is installed, and then use the following command to migrate, which will migrate `all inbound account data` of v2-ui of this machine to x-ui, `panel settings and username and password will not migrate`

> After the migration is successful, please `close v2-ui` and `restart x-ui`, otherwise the inbound of v2-ui and the inbound of x-ui will produce a `port conflict`

```
x-ui v2-ui
```
## issue closed

All kinds of white questions make blood pressure very high

## Stargazers over time

[![Stargazers over time](https://starchart.cc/vaxilu/x-ui.svg)](https://starchart.cc/sina-sec/x-ui)
