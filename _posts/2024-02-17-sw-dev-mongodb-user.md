---
title: (MongoDB) MongoDB 사용자(유저, 계정) 관리
date: 2024-02-17 20:00:00:00 +0900
categories: [SW Development, Backend]
tags: [swdev, mongodb, account, user]     # TAG names should always be lowercase
--- 

### MongoDB 계정 
MongoDB는 기본적으로 사용자가 등록되어 있지 않으며, <br> 
사용자의 이름과 암호 없이 모든 데이터베이스에 접근이 가능함.<br>
이 상태에서 mongosh 역시 그냥 mongosh 명령만 입력하면 접속이 된다.

### 사용자 계정 만들기
사용자계정은 MongoDB 내부에 생성 된 Database 마다 별도로 관리됨.<br>
이러한 계정 정보는 db.system.users 컬렉션에 저장된다.
> 사전조건<br>
  1. 관리자 계정 생성
      - admin Database에 관리자 권한을 가진 계정을 생성한다.
      - userAdminAnyDatabase와 readWriteAnyDatabase 권한이 부여되어야 함.<br>
        ``` bash
        > use admin
        > db.createUser( {
          user: "mongoadmin",
          pwd: passwordPrompt(), // cleartext password
          roles: [
              { role: "userAdminAnyDatabase", db:"admin"},
              { role: "readWriteAnyDatabase", db:"admin"}
          ]
        })
        ```
  2. 접근 제어 활성화 : <br>
      [(cf) docker-compose로 설치할 경우 root/pass지정하면 mongod.conf를 수정하지 않아도 된다.]({% post_url 2023-09-06-sw-dev-mongodb-installation %})
      - 설정파일(/etc/mongod.conf)을 수정하고 MongoDB 데몬 재실행<br>
        ``` bash
        $ vi /etc/mongod.conf
              security:
                 authorization: enabled
        ```

### 사용자 계정 조회
```  bash
//mongosh 에서
> show users  //  전체사용자조회 or db.getUsers()
> db.getUsers("", {showPrivileges: true}) //특정user의 정보를 조회
```

### 일반계정 생성
``` bash
> mongosh --port 27017 --authenticationDatabase "admin" -u mongoadmin -p xxxxx   //admin계정으로 mongosh접속후 아래 명령어 수행
> db.createUser( {
  user: "guest",
  pwd: "123456", 
  roles: [
      { role: "read", db: "dbname" }
  ]
})
```