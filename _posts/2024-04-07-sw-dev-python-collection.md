---
title: (PYTHON) collections
date: 2024-04-07 16:00:00:00 +0900
categories: [SW Development, Programming Language]
tags: [swdev, python, collection]     # TAG names should always be lowercase
--- 

### collection
> List, Tuple, Dictionary, Set<br>

5. List : [ ] <br>
Python의 리스트는 1-Dimension 구조 이다. 다차원처럼 쓰기위해 리스트 안에 리스트를 중첩해서 쓴다.<br>
2중['a', ['b'], ['c','d']] <br>
3중['a', ['b','c'], ['d','e',['f']]]<br>
다차원을 사용하려면 numpy의 ndArray를 사용한다.
- [list comprehension](https://doorbw.tistory.com/174)
``` python
%time
list_arr = [i for i in range(1000000)] # 이와같이사용하는 게 list comprehension, 표현간결
```
- list() : 비어있는 리스트 생성 a = [] 와 동일
- sort와 sorted
- len, sum, max, min
- slicing : 연속적인 객체들에(예: 리스트, 튜플, 문자열) 범위를 지정해 선택해서 객체들을 가져오는 방법 및 표기법을 의미. 
            슬라이싱을 하면 새로운 객체를 생성. 즉, 일부분을 복사해서 가져옴. <br> 
            기본사용: a[start : end : step] --> start (시작인덱스), end (끝나는인덱스),step(보폭)<br>
                        
            a = ['a', 'b', 'c', 'd', 'e']
            // Index References
            -------------------------------
            |  a  |  b  |  c  |  d  |  e  |
            -------------------------------
            |  0  |  1  |  2  |  3  |  4  |          // 양수의 경우
            -------------------------------
            | -5  | -4  | -3  | -2  | -1  |          // 음수의 경우
            -------------------------------
            a[ 1 :  ]         # ['b', 'c', 'd', 'e']  start는 포함
            a[  : -1 ]        # ['a', 'b', 'c', 'd'], end는 포함하지 않음
            a[ 2 : 4 ]        # ['c', 'd']
            a[ : : 2 ]        # 2칸씩 이동하면서 가져옵니다. ['a', 'c', 'e']
            a[ -5 : : 3 ]     # 3칸씩 이동하면서 가져옵니다. ['a', 'd']
            a[ : : -1 ]       # 전체를 거꾸로 가져옵니다. ['e', 'd', 'c', 'b', 'a']
            

2. Tuple : ( )<br>
List보다 초기화가 간결, 리스트는 요소 값의 생성, 삭제, 수정이 가능하지만, **튜플은 요소값을 바꿀 수 없다.**
``` python
a, b, c = 1,2,3 # a=1, b=2, c=3 이렇게 초기화 하지 않아도 된다.
a, b = map(int, input().split()) # map과함께 입력값을 commandline에서 입력받아 a, b값을 초기화.
a, b = 3, 7  # a에 3, b에 7 값으로 초기화
a, b = b, a  # a, b값이 서로의 값을 교환함 a=7, b=3, swap을 바로 할 수 있음.
```

7. Dictionary : { }<br>
사전, key와 value 로 저장됨

8. Set : { } <br>
Dictionary와 표기가 같다. 순서가 없다. 따라서 **인덱스가 없고 인덱싱 불가능. 중복 허용 안됨.**
- set(), add(), update(), remove(), clear() in(), len(),discard(), pop()
- instersection(), union(), difference(), issubset()