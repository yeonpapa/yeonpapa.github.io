---
title: (PYTHON) 자료형
date: 2024-03-04 16:00:00:00 +0900
categories: [SW Development, Programming Language]
tags: [swdev, python, variables]     # TAG names should always be lowercase
--- 

### 자료형의 종류
> Integer, Float, String, Boolean, List, Tuple, Dictionary, Set<br>

1. Integer<br>
파이썬에서 Integer는 값의 범위가 무한임.overflow가 안생김. 주의할 점은 사칙연산시에 나누기 연산의 경우, Integer가 float이 된다.<br>
``` python
num = 3 / 3
type(num)   # 결과 : 1.0 으로 float임 
type(3//3)  # 결과 : int , 결과를 정수로 받으려면 '//'  연산자를 사용하거나
divmod(7,3) # 결과 : (2, 1) divmod를 사용하여 목과 나머지로 나누어 생각해줘야 함.
```
2. Float<br>
실수오차가 발생할 수 있다. 파이썬에서 0.1 + 0.2의 값은? 0.3이 나올 것 같지만 실제로는 0.30000000000000004가 나옵니다. 
파이썬은 실수를 부동소수점 방식으로 표현하는데 부동소수점은 실수를 정확히 표현할 수 없는 문제가 있습니다. 
그래서 정확히 0.3이 아닌 0.30000000000000004가 나옵니다
유리수(분수)의 경우는 tuple형식으로 분자 분모를 따로 저장하는게 좋다.<br>
``` python
result = 0.1 + 0.2 # 0.3을 기대하지만,
print(result)      # 0.30000000000000004
if 0.1 * 3 == 0.3 : # true 를 기대하지만, False임.
```
3. String<br>
immutable(변경되지않는) 변수로 스트링 연산을 할 경우는 join, split, replace, find등의 함수를 사용하는게 좋다.
+,* 보다는 join을 사용. string의 slice를 활용 할 수도 있다.
<br>

4. Boolean<br>
코드최적화에 short circuit으로 활용

5. Container - List <br>
- [list comprehension](https://doorbw.tistory.com/174)
``` python
%time
list_arr = [i for i in range(1000000)] # 이와같이사용하는 게 list comprehension, 표현간결
```
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
            

6. Container - Tuple <br>
List보다 초기화가 간결
``` python
a, b, c = 1,2,3 # a=1, b=2, c=3 이렇게 초기화 하지 않아도 된다.
a, b = map(int, input().split()) # map과함께 입력값을 commandline에서 입력받아 a, b값을 초기화.
a, b = 3, 7  # a에 3, b에 7 값으로 초기화
a, b = b, a  # a, b값이 서로의 값을 교환함 a=7, b=3, swap을 바로 할 수 있음.
```

7. Container - Dictionary <br>
사전, key와 value 로 저장됨

8. Container - Set<br>