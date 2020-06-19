---
layout: post
title: 高可靠/带有负载均衡的CockroachDB搭建
description: Nope
tag: 产品开发
---

### CockroachDB搭建

简介:


### 环境准备

机器:
· satellive01(192.168.1.100)

· satellive03(192.168.1.106)

· satellive04(192.168.1.110) 改成192.168.1.104

· satellive05(192.168.1.107)

四台机器环境均为: Ubuntu 18.04

各机器之间网络通信设置:

· 检测网络通信是否正常(默认为正常)

· 防火墙开启26257和8080端口
```
sudo apt-get install ufw
%sudo ufw enable // 开启ufw防火墙配置
sudo ufw allow 26257
sudo ufw allow 8080

sudo ufw status // 检验端口状态
```

### 文件准备

将CockroachDB所有的相关文件放在/opt/cockroach下面, 该目录下, 我们
准备bin(执行文件)、etc(配置文件)、dat(数据文件)、log(日志文件)四个文件夹.
然后从官网下载最新的cockroachdb

```
cd /opt
mkdir cockroach
cd cockroach
mkdir bin etc log dat
wget https://binaries.cockroachdb.com/cockroach-v19.2.6.linux-amd64.tgz
tar xzvf cockroach-v19.2.6.linux-amd64.tgz
mv cockroach-v19.2.6.linux-amd64/cockroach bin/
rm cockroach-v19.2.6.linux-amd64 cockroach-v19.2.6.linux-amd64.tgz -rf
```

### 生成安全证书

在Satellive01上生成根证书, 再拷贝到其他节点上.

生成根证书:
```
cd /opt/cockroach/
mkdir -p etc/certs etc/my-safe-directory
bin/cockroach cert create-ca --certs-dir=etc/certs --ca-key=etc/my-safe-directory/ca.key

// 命令执行完毕后, 会生成根证书的钥匙: etc/certs/ca.crt和etc/my-safe-directory/ca.key
// 这两个文件非常重要, 需要妥善保管; ca.key是私钥, 需要保密, 所以集群搭建完成后, 需要从各个节点
// 删除ca.key, 避免私钥泄露, 以后需要扩容添加节点时, 再取出保管好的ca.crt和ca.key
```
