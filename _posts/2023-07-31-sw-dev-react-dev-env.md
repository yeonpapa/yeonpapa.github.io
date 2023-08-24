---
title: (REACT) 개발환경
date: 2023-07-31 10:00:00:00 +0900
categories: [SW Development, Frontend]
tags: [swdev, react, devenv]     # TAG names should always be lowercase
--- 

### Node.js(NPM), vs code 설치
> **Node.js**는 자바스크립트로 네트워크 애플리케이션을 개발할 수 있도록 해주는 환경<br>
**NPM방식** 개발을 위해서는 node.js를 설치해서 개발함 (vs **CDN방식**)
1. [Node.JS 설치](https://nodejs.org/en/)<br>
```shell
$ node --version
$ npm --version
```
2. create-react-app 설치
```shell
$ npm install -g create-react-app
```
3. project 생성 후 실행
```shell
$ mkdir workdir
$ cd workdir
workdir$ npx create-react-app hello-world
workdir$ cd hello-world
workdir\hello-world$ npm start
```
4. Route 사용하기 위해서는 아래 설치 후 App.js에 <br/>
```import {BrowserRouter as Router, Route, Routes} from 'react-router-dom'``` 추가.
```shell
$ npm install react-router-dom
```
5. Bootstrap 사용하기위해서는 아래 설치 후 App.js에 <br/>
```import 'bootstrap/dist/css/bootstrap.min.css';``` 추가. 
관련문서:[BootStrap](https://www.w3schools.com/bootstrap5/) , [ReactStrap](https://reactstrap.github.io/)
```shell
$ npm install --save reactstrap
$ npm install --save bootstrap
```

> [VS Code 설치](https://code.visualstudio.com/)
1. react extension 설치 : ESLint, Reactjs code snippets, Relative Path, Guides
2. JS 파일에서 emmet 설정 (코드 단축키 제공)
   - VS Code의 File -> Preferences -> Settings
   - Settings 검색창에서 'includel' 입력
   - key:javascript, value:javascriptreact 입력