# x-ui
[简体中文](./README.md)| ENGLISH 

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

```
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
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

## SSL certificate application

> This function and tutorial are provided by [sina-sec](https://github.com/sina-sec)

The script has a built-in SSL certificate application function. To use this script to apply for a certificate, the following conditions must be met:

- Know the Cloudflare registered email address
- Know Cloudflare Global API Key
- The domain name has been resolved to the current server through cloudflare

How to get Cloudflare Global API Key:
    ![](media/bda84fbc2ede834deaba1c173a932223.png)
    ![](media/d13ffd6a73f938d1037d0708e31433bf.png)

When using it, you only need to enter `domain name`, `email`, `API KEY`, the schematic diagram is as follows:
        ![](media/2022-04-04_141259.png)

Precautions:

- The script uses the DNS API for certificate requests
- Use Let'sEncrypt as the CA party by default
- The certificate installation directory is the /root/cert directory
- The certificates applied for by this script are all wild domain name certificates

##Use of Tg robot (under development, temporarily unavailable)

> This function and tutorial are provided by [sina-sec](https://github.com/sina-sec)

X-UI supports daily traffic notification, panel login reminder and other functions through Tg robot. To use Tg robot, you need to apply for it yourself
For specific application tutorials, please refer to [Blog Link] (https://coderfan.net/how-to-use-telegram-bot-to-alarm-you-when-someone-login-into-your-vps.html)
Instructions for use: Set robot-related parameters in the background of the panel, including

- Tg Robot Token
- Tg Bot ChatId
- Tg robot cycle running time, using crontab syntax

Reference syntax:
- 30 * * * * * //Notify on the 30th of every minute
- @hourly // hourly notification
- @daily //Notification every day (0:00 AM)
- @every 8h // notify every 8 hours

TG notification content:
- Node traffic usage
- Panel login reminder
- Node expiration reminder
- Traffic warning reminder

More functions are planned...
## Suggestion system

- CentOS 7+
- Ubuntu 16+
- Debian 8+

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
