---
title: Pandas - lambda and apply
date: 2023-06-04 14:00:00 +0900
categories: [Data Analysis and Python Libs, Data Wrangling]
tags: [pandas, apply, lambda]     # TAG names should always be lowercase
--- 

##### lambda
> (lambda  인수 : 함수)
<br> lambda 뒤에 나오는 인수는 함수에서 사용될 변수들을 정의하며
<br> 인수에서 정의 된 변수를 함수에 적용시킨 결과를 도출한다.
```
(lambda x, y : x + y)(5, 2) ##인수인 x와 y를 'x + y'에 넣어 계산
## 이때, 각 인수의 실재 값을 인자로 넣어서 계산한다.
>> 7  ##계산결과
```
```
df = pd.DataFrame(columns = ['a','b'], data = [[1,2], [2,3], [3,4]])
>>
	a	b
0	1	2
1	2	3
2	3	4
df['c'] = (lambda x,y : x + y)(df['a'], df['b'])
>>
	a	b	c
0	1	2	3
1	2	3	5
2	3	4	7
```

##### apply
> apply는 2차원 타입의 데이터에서 행/열 또는 전체에 원하는 연산을 지원한다.
<br>행 단위로 연산을 하고싶은 경우 axis = 1, 열 단위로 연산을 하고싶은 경우는 axis = 0으로 설정한다.
<br>기본값은 axis = 0을 설정되어 있다.
```
df
>>
	a	b	c
0	1	2	3
1	2	3	5
2	3	4	7
--------------------------------------------------------
import numpy as np
df.apply(np.average, axis = 1)
>>
0    2.000000
1    3.333333
2    4.666667
dtype: float64
--------------------------------------------------------
df.apply(np.average, axis = 0)
>>
a    2.0
b    3.0
c    5.0
dtype: float64
--------------------------------------------------------
df['hi'] = df.a.apply(lambda x : str(x) + 'hi')
df
>>
	a	b	c	hi
0	1	2	3	1hi
1	2	3	5	2hi
2	3	4	7	3hi
```