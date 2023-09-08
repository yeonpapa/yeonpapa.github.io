---
title: (Ubuntu) Java, Python 설치
date: 2023-09-08 11:00:00:00 +0900
categories: [SW DevOps, OS]
tags: [swdevops, linux, ubuntu, java, python]     # TAG names should always be lowercase
--- 

## Java 11 설치
```shell
$ sudo apt-get update
$ sudo apt-get upgrade

# JAVA11 설치
$ sudo apt-get install openjdk-11-jdk
$ java -version
```

## Python 3.10 설치
1. apt로 설치
```shell
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository ppa:deadsnakes/ppa
$ sudo apt update
$ sudo apt install python3.10
$ sudo apt-get install python3-pip #pip가 설치가 안됨, 따로 설치해줘야
$ python3.10 --version
```

2. wget 매뉴얼설치
``` shell
$ wget https://www.python.org/ftp/python/3.10.3/Python-3.10.3.tgz
$ tar -xf Python-3.10.*.tgz
$ cd Python-3.10.*/
./configure --enable-optimizations
$ make -j $(nproc)
$ sudo make altinstall
$ python3.10 --version
```