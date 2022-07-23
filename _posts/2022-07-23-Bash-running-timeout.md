---
layout: post
title: Network adapter running timeout
categories: [Linux, Shell]
description: Running timeout
keywords: Linux, shell, running, timeout, network
---

## 函数

```shell
# $1:dev name; $2 time(s),default 3s;
function _running_timeout(){
	local i=${2:-3};
	while (( i > 0 ))
	do
	    if ifconfig "$1" | grep -i running; then
	        return 0;
	    fi
	    ((i--));
	    sleep 1;
	done
	return 1;
}
```

## 用法示例1:

检测网卡 eth0 是否为 running 状态；

running 即立即打印 OK，不 running 则打印 Error。

```shell
if _running_timeout "eth0"; then
	echo "OK"
else
	echo "Error"
fi
```

## 用法示例2:

检测网卡 eth0 是否为 running 状态，超时5秒；

一旦 running 即立即打印 OK，若等 5 秒还不 running 则打印 Error。

```shell
_running_timeout "eth0" 5 && echo "OK" || echo "Error"
```


