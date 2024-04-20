---
title: (PYTHON) for, while
date: 2024-04-20 16:00:00:00 +0900
categories: [SW Development, Programming Language]
tags: [swdev, python, loop]     # TAG names should always be lowercase
--- 

### loop
> for, while<br>

1. for <br>
**for** 변수 **in** 리스트(또는 튜플, 문자열)<br>

- basic

``` python
a = [(1,2), (3,4), (5,6)]
for (first, last) in a:
    print(first + last)

add = 0 
for i in range(1, 11): # 1부터 10까지 더하기
add = add + i 

a = [1,2,3,4]
result = [num * 3 for num in a]
print(result) #결과: [3, 6, 9, 12]
```

- enumerate, zip
<br>

``` python
numbers = [1, 2, 3]
letters = ["A", "B", "C"]

for pair in zip(numbers, letters):
    print(pair)
# print(pair) 결과
#(1, 'A')
#(2, 'B')
#(3, 'C')

# enumerate - 인덱스와 값을 같이 리턴함.
for i in range(len(letters)):
    letter = letters[i]
    print(i, letter)
# 위 문장을 아래로 변경. 동일함
for i, val in enumerate(letters):
    print(f'enumerate:idx-{i}, val-{val}')
# 출력
# enumerate:idx-0, val-A
# enumerate:idx-1, val-B
# enumerate:idx-2, val-C
for i, val in enumerate(letters, start=10):
    print(f'enumerate:idx-{i}, val-{val}')
# 출력
# enumerate:idx-10, val-A
# enumerate:idx-11, val-B
# enumerate:idx-12, val-C

# zip 함수 참고
print(f'list:{list(zip(numbers, letters))}') # list:[(1, 'A'), (2, 'B'), (3, 'C')]
print(f'dict:{dict(zip(numbers, letters))}') # dict:{1: 'A', 2: 'B', 3: 'C'} 
# --  zip(,) zip파라메터의 순서대로 키:값 이 된다.
# unzip -- unpacking...결과는 전부 튜플로 리턴됨
aZippedlist = list(zip(numbers, letters))
n, l = zip(*aZippedlist) #unzip이 된다.

print(f'aZippedlist:{aZippedlist}') # aZippedlist:[(1, 'A'), (2, 'B'), (3, 'C')]
print(n) #(1, 2, 3)
print(l) #('A', 'B', 'C')
```

- under bar(_)
<br>

``` python
for _ in range(5):
	print("Hello World") # "Hello World" 5회 출력
## list 초기화 0으로..
mlist = [ 0 for _ in range(10)] # 변수로 넘어 오는 값을 사용하지 않고 그냥 loop만 돌림.
print(mlist) # [0,0,0,0,0,0,0,0,0,0]
```
<br>

2. while <br>
while 조건문:<br>
    수행할_문장1<br>
    수행할_문장2<br>
    수행할_문장3<br>

``` python
a = 0
while a < 10:
    a = a + 1
    if a % 2 == 0: continue
    print(a)
```

``` python
coffee = 10
money = 300
while money:
    print("돈을 받았으니 커피를 줍니다.")
    coffee = coffee - 1
    print("남은 커피의 양은 %d개입니다." % coffee)
    if coffee == 0:
        print("커피가 다 떨어졌습니다. 판매를 중지합니다.")
        break
```