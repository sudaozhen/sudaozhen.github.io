---
layout: post
title: Ping timeout
categories: [Linux, Shell]
description: Ping timeout
keywords: Linux, shell, ping, timeout
---

## 函数

```shell
#$1:ip; $2:time(s),default 0.2s;
function _ping_timeout(){
    local i=${2:-1};
    if [ -z "$2" ]; then
    	local j=0.2;
    else
    	local j=1;
    fi
    while ((i > 0))
    do
        timeout "$j" ping -c 1 "$1" &>/dev/null 2>&1 && return 0;
        ((i--));
    done
    return 1;
}
```

## 用法示例1:

ping 192.168.1.1 超时0.2秒，ping通打印 OK，ping不通打印 Error。

```shell
if _ping_timeout "192.168.1.1"; then
	echo "OK"
else
	echo "Error"
fi
```

## 用法示例2:

ping 192.168.1.1 超时0.2秒，通打印 OK，不通打印 Error。

```shell
_ping_timeout "192.168.1.1" && echo "OK" || echo "Error"
```

## 用法示例3:

ping 192.168.1.1 ，只要 ping 通立即打印 OK；

ping 10 秒还不通，打印 Error。

```shell
if _ping_timeout "192.168.1.1" 10 ; then
	echo "OK"
else
	echo "Error"
fi
```

