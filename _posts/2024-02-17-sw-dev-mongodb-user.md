---
title: (MongoDB) MongoDB 사용자(유저, 계정) 관리
date: 2024-02-17 20:00:00:00 +0900
categories: [SW Development, Backend]
tags: [swdev, mongodb, account, user]     # TAG names should always be lowercase
--- 

### MongoDB 계정 
MongoDB는 기본적으로 사용자가 등록되어 있지 않으며, <br> 
사용자의 이름과 암호 없이 모든 데이터베이스에 접근이 가능함.

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
          user: "계정이름",
          pwd: passwordPrompt(), // cleartext password
          role: [
              { role: "userAdminAnyDatabase", db:"admin"},
              { role: "readWriteAnyDatabase", db:"admin"}
          ]
        })
        ```
  2. 접근 제어 활성화
      - 설정파일(/etc/mongod.conf)을 수정하고 MongoDB 데몬 재실행<br>
        ``` bash
        $ vi /etc/mongod.conf
              security:
                 authorization: enabled
        ```