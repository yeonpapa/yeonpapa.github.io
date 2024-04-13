---
title: (PYTHON) 자료형
date: 2024-03-04 16:00:00:00 +0900
categories: [SW Development, Programming Language]
tags: [swdev, python, variables]     # TAG names should always be lowercase
--- 

### 자료형의 종류
> Integer, Float, String, Boolean<br>

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