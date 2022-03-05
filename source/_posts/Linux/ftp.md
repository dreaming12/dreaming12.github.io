---
title: ftp
date: 2022-03-04
---

# FTP

## HOW TO BUILD

> Ubuntu 20.04
> 
> [vsftpd](https://security.appspot.com/vsftpd.html#about) ~ [Doc](https://security.appspot.com/vsftpd/vsftpd_conf.html)
> 
> 由于不是 `root` 用户，需要使用命令 `sudo`

```shell
$ sudo install vsftpd
$ sudo systemctl enable vsftpd # 开机自启
$ sudo systemctl start vsftpd # 启动服务
$ sudo netstat -antup | grep ftp # 确认服务是否启动
```

```shell
$ sudo useradd hello # 为 FTP 服务创建一个用户 hello
$ sudo passwd hello # 设置用户的密码
$ sudo mkdir /home/hello
$ sudo chown -R hello:hello /home/hello # 修改目录权限
```

由于大多数客户端机器的防火墙设置及无法获取真实 IP 等原因，建议选择被动模式搭建 FTP 服务

```shell
$ sudo vim /etc/vsftpd.conf # 修改配置文件
```

```conf
# 取消注释
listen=YES
anonymous_enable=NO
write_enable=YES
local_enable=YES
chroot_local_user=YES
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd.chroot_list

# 添加注释
# listen_ipv6=YES

# 添加配置
local_root=/home/hello
allow_writeable_chroot=YES
pasv_enable=YES
pasv_address=xxx.xx.xxx.xx # 服务器公网 IP
pasv_min_port=40000 # 可修改
pasv_max_port=45000
```

```shell
# 输入用户名，一个用户名占据一行，设置的用户将不会被锁定在主目录
$ sudo vim /etc/vsftpd.chroot_list 
$ sudo systemctl restart vsftpd
```

设置安全组，开放对应端口（21 & 40000-45000）

## PROBLEMS

:heavy_exclamation_mark: 没有安全方面的配置

:heavy_exclamation_mark: `500 Illegal PORT command" using command-line ftp`

Linux command-line ftp defaults to using active-mode FTP. Try switching to passive mode with the `pass` command.

:tada:

## COMMANDS

```shell
$ ftp [ip]

$ ftp
ftp> open [ip]

ftp> ? # help
ftp> help [command]

ftp> ! # escape to the shell
# you can use command exit to go back to ftp

ftp> get [filename]

ftp> put [filename]

ftp> bye # quit
````
