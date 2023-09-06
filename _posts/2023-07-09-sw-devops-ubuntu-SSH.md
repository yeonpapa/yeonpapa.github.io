---
title: (Ubuntu) SSH Server
date: 2023-07-09 11:00:00:00 +0900
categories: [SW DevOps, OS]
tags: [swdevops, linux, ubuntu, ssh]     # TAG names should always be lowercase
--- 

## SSH 설치와 접속방법 
0. Open SSH Server 설치
   - ```$ sudo apt update```
   - ```$ sudo apt install openssh-server```
1. SSH Server
   - ssh 서비스가 실행 중 인지 확인 ```$ sudo systemctl status ssh```
   - active (running) 이면 실행 중
2. SSH enable / start (서비스가 inactive이면 아래 명령어로 enable,start시킴)
   - ```$ sudo systemctl enable ssh```
   - ```$ sudo systemctl start ssh```
3. SSH Client
   - ```$ sudo apt-get install openssh-client```
   - ```$ ssh username@ip_address```
   - (포트지정할 경우) ```$ ssh -p 10001 username@ip_address```
4. Firewall
   - 방화벽 상태 확인 ```$ sudo ufw status```
   - 방화벽에서 ssh 허용 ```$ sudo ufw allow ssh```
5. SSH port변경
   - SSH를 외부에 노출할떄는 22번 포트가 아닌 다른 포트로 변경하는 것이 좋음
   - **/etc/ssh/sshd_config** 파일 수정, Port는 여러개 지정가능
   ```bash
   ## ssh 포트
   ## Port 22
   Port 10022
   Port 20022 
   ```
   ```$ sudo systemctl restart sshd``` or ```$ sudo service sshd restart```

<br/>
## 참고

| 명령어종류 | systemctl | service |
|-------|:---:|:---:|
| 서비스 상태확인 | systemctl status **서비스명** | service **서비스명** status |
| 서비스 시작 | systemctl start **서비스명** | service **서비스명** start |
| 서비스 정지 |systemctl stop **서비스명** | service **서비스명** stop |
| 서비스 재시작 |systemctl restart **서비스명** | service **서비스명** restart |
| 서비스 리로드 |systemctl reload **서비스명** | service **서비스명** reload |

## 참고 -
1. root계정 활성화
```
$ sudo passwd root
New password:
Retype new password:
passwd: password updated successfully
```
2. root계정 ssh 로그인 활성화 
```
$ vi /etc/ssh/sshd_config '#PermitRootLogin prohibit-password' 값을 'PermitRootLogin yes'으로 변경
```
