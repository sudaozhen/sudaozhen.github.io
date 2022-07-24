---
layout: wiki
title: Shell 常用函数
cate1: Shell
cate2: Linux
categories: Shell
description: Shell 常用函数
keywords: shell, 函数, function, Linux
---

## 进度条

```shell

#!/bin/bash
function _bar() {
    local num=0
    local str=''
    local max=100
    local postfix=('|' '/' '-' '\')
    local index
    while [ $num -le $max ]
    do
        ((index=num%4))
        printf "[%-50s %-2d%% %c]\r" "$str" "$num" "${postfix[$index]}"
        ((num++))
        # sleep "$( echo "scale=1; $1/$max" |bc )"
        sleep "$(awk 'BEGIN{ printf "%.2f\n",'"$1"'/'$max'}')"
        if ((num % 2 == 0)); then
        	str+='#'
        fi
    done
    printf '\n'
}

function _bar_wait(){
    while [ "$(ps aux | awk '{print $2}' |grep -c $1)" != "0" ]
    do
        sleep 0.2
    done
    _info "Done!"
}

sleep 30 & #后台任务
BG_PID=$!
_bar 30
_bar_wait $BG_PID
```



## 打印颜色

```shell
function _red() {
	printf '\033[1;31;31m%b\033[0m' "$1"
}
function _green() {
	printf '\033[1;31;32m%b\033[0m' "$1"
}
function _yellow() {
	printf '\033[1;31;33m%b\033[0m' "$1"
}
function _magenta() {
	printf '\033[1;31;35m%b\033[0m' "$1"
}
function _info() {
    _green "[Info] "
    printf -- "%s" "$1"
    printf "\n"
    _log "[Info] $1"
}
function _warn() {
    _yellow "[Warning] "
    printf -- "%s" "$1"
    printf "\n"
    _log "[Warning] $1"
}
function _error() {
    _red "[Error] "
    printf -- "%s" "$1"
    printf "\n"
    _log "[Error] $1"
    echo "For more details, please check the log file: ${LOG_FILE_NAME}" 
    exit 1
}

```

## 日志输出

```shell
LOG_DIR="/var/log"
LOG_FILE_NAME="taet.log"
_log() {
    #judge the params,it must 2 params;
    if [ 1 -gt $# ]; then
        echo  "WARN parameter not correct in log function"
        return;
    fi
    #如果日志的根目录不存在，则应该先创建
    if [ ! -d $LOG_DIR ];then
        mkdir -p $LOG_DIR
    fi
    #判断日志文件是否存在，不存在则创建
    if [ ! -e "$LOG_FILE_NAME" ];then
        touch $LOG_FILE_NAME
    fi
    #日志时间
    local curtime
    curtime=$(date +"%F %T")
    #判断日志的大小，然后如果对于指定的行数，则应该备份旧的日志文件，然后创建新的日志文件
    local cursize
    if [ ! -e "$LOG_FILE_NAME" ];then
        echo "There is no log file!Not record log to file!"
        return
    fi
    # 计算现有的日志文件的行数
    cursize=$(cat $LOG_FILE_NAME | wc -c)
    if [ $FSIZE -lt "$cursize" ];then
        echo "backup old log file"
        # 备份文件名为：日期.log
        mv $LOG_FILE_NAME "$curtime"".log"
        # 创建新的日志文件
        touch $LOG_FILE_NAME
    fi  
    # 打印控制台日志和记录日志到文件
    echo "$curtime $*">> $LOG_FILE_NAME
}
```

## 脚本参数输入

```shell
#!/bin/bash
while getopts "T:" args
do
    case $args in
    T)
        test=$OPTARG
        #echo "aaa" $test
        while [ -n "$(echo $test | awk -F , '{print $2}')" ]
        do 
            out=$out' '$(echo $test | awk -F , '{print $1}')
            test=$(echo $test | sed 's/[0-9-]*,//')
            #test=${test//[0-9]*,/}
        done
            #echo $test
            if echo "$test" | grep  -q '^[[:digit:]]*$' ; then
            	out=$out' '$(echo $test)
            else
            	echo "error"
            exit 1
            fi
        ;;
    *)
    	;;
    esac
done
echo $out
```

## 后台输出“.”

```shell
#!/bin/bash

function _dots(){
    local seconds
    seconds=${1:-1}
    while :
    do
        #printf a dot every 5 seconds by default
        sleep "$seconds"
        echo -n '.'
    done
}

_dots 1 &
BG_PID=$!
trap "kill -9 $BG_PID" INT
sleep 150 #do somthing
kill $BG_PID
echo
```

## 检查用户密码

```shell
user="root"
passwd_list="123456 123123 321321"
function _check_user_passwd ()
{
    local i;
    for i in $passwd_list
    do
    	if sshpass -p "$i" ssh -o StrictHostKeyChecking=no $user@localhost "exit" &>/dev/null 2>&1;then
            passwd=$i;
            #printf "$user passwd:%s\r\n" $passwd;
            return 0;
    	fi;
    done
    while :
    do
        read -rp "Please enter the password of $user:" passwd;
        sshpass -p "$passwd" ssh -o StrictHostKeyChecking=no $user@localhost "exit" &>/dev/null 2>&1 && return 0;
    done
    return 1;
}

```

## ping超时

```shell
#$1:ip; $2:time(s),default 0.2s
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

## 网卡running超时

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

