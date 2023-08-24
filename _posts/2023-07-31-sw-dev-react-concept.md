---
title: (REACT) 정의와 개념
date: 2023-07-31 11:00:00:00 +0900
categories: [SW Development, Frontend]
tags: [swdev, react,concept]     # TAG names should always be lowercase
--- 

### React 정의
> React : A Javascript library for building user interface <br>
대표적인 Javascript UI library, JQuery도 이에 해당한다.<br>
1. AngularJS 프레임워크
2. React 라이브러리
3. Vue.js 프레임워크

### SPA (Single Page Application)
> 하나의 페이지만 존재하는 웹사이트<br>
규모가 큰 웹사이트의 경우 수백개의 페이지가 존재하는데, 이모든 페이지를 
HTML로 만드는 것은 비효율적임. 따라서 하나의 페이지를 만들고 그 BODY안에
여러 요청에 대응하는 Contents를 채워서 보여주는 방식을 말함.
React는 이를 쉽고 빠르게 만들 수 있도록 해주는 도구<sup>library</sup> 임.

### Pros and Cons
> 1. Pros <br>
     - 빠른 업데이트와 렌더링 속도(UI갱신)<sup>**Virtual DOM**</sup>
     - 컴포넌트 기반 구조<sup>Component Based Development</sup>
     - 재사용성<sup>Resusability</sup>
     - Meta<sup>facebook</sup>의 지원
     - 활발한 커뮤니티
     - 모바일 앱개발 가능<sup>**React Native**</sup>
  2. Cons
     - 방대한 학습량
     - 높은 상태<sup>**state**</sup> 관리 복잡도 - Redux, MobX, Recoil