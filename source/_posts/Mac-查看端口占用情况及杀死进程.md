---
title: Mac 查看端口占用情况及杀死进程
date: 2020-03-18 11:25:23
tags:
---
突然碰到服务起不来的情况，想查看一下端口占用情况，发现竟然忘了命令。就怕长时间不用，不用，就会忘啊。

查看端口占用情况命令
```bash
sudo lsof -i :8000
```
冒号后面就是你需要查看的端口号。
```bash
COMMAND   PID USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
node    36318 King   31u  IPv4 0xe67b06f3bbf6e085      0t0  TCP *:irdmi (LISTEN)
```
如上图。有一个表头名为PID的一列，这一列就表示占用当前端口的进程。
杀掉占用当前端口号的进程
```bash
sudo kill -9 36318
```
-9后面加一个空格，然后加上占用端口的进程PID，就可以杀掉占用端口的进程。最后重启就ok。
