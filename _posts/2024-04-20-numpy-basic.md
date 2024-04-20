---
title: Numpy - basic
date: 2024-04-20 18:00:00 +0900
categories: [Data Analysis and Python Libs, Data Wrangling]
tags: [numpy,basic]     # TAG names should always be lowercase
--- 

##### **numpy-ndArray**
1. ndArray
> n차원 array, 배열 요소의 타입은 동일해야함. 다른 타입의 데이터가 하나의 array에 들어갈 수 없음.<br> 파이썬에서 
n차원을 지원하는 자료형은 numpy의 ndArray임. list, tuple등은 n차원이 아니라 2중첩, 3중첩 리스트임.

2. 사용방법

``` python
import numpy as np
data1 = [8, 2, 3.3, 9, 10] # python list
# ndArray 초기화
arr = np.array(data1)
arr2 = np.array(data1, dtype=np.int32) # type을 지정할 수 있다., 배열의 요소는 모두 동일한 타입
print(arr)  #[ 8.   2.   3.3  9.  10. ], type이 자동을 float로 맞춰짐
print(arr2) #[ 8  2  3  9 10], 지정한 int type으로 들어감
print(type(arr)) #자료구조의 타입, <class 'numpy.ndarray'>
print(type(arr.dtype)) #자료구조 내의 데이터 타입, <class 'numpy.dtype[float64]'>
print(type(arr2.dtype)) #자료구조 내의 데이터 타입, <class 'numpy.dtype[int32]'>

data2 = [[1,2,3],[4,5,6]] # python의 list는 2차원이 없다. 2차원 처럼 쓰는 것임. 2중(첩) 리스트
print(data2) #[[1, 2, 3], [4, 5, 6]]
arr2 = np.array(data2) #ndArray가 진짜 n차원 임.
print(arr2) 
#결과
#[[1 2 3]
# [4 5 6]]
print(arr2.shape) #(2, 3) 2행 3열

# numpy array 생성방법 들...
print(np.array([[2,4,1], [6,7,8]]))
#[[2 4 1]
# [6 7 8]]
print(np.arange(0,10,1)) # [0 1 2 3 4 5 6 7 8 9]
print(np.linspace(-3,3,5)) # [-3.  -1.5  0.   1.5  3. ], -3부터 3사이를 5개의 값으로 나눔
print(np.ones((3, 4))) # shape 을 (행,열) 이렇게해도 되고 [행,열] 된다.
#[[1. 1. 1. 1.]
# [1. 1. 1. 1.]
# [1. 1. 1. 1.]]
print(np.ones((2))) # [1. 1.] , 1로 초기화
print(np.zeros((2))) # [0. 0.] , 0으로 초기화
print(np.zeros((2, 3)))
#[[0. 0. 0.]
# [0. 0. 0.]]
print(np.empty(shape=(10,), dtype=np.int8)) # 가장나중에있는 메모리의 값이 채워짐...사용안하는게 좋음
print(np.full((3, 4),100)) # 지정한 값으로 초기화
#[[100 100 100 100]
# [100 100 100 100]
# [100 100 100 100]]

## array의 indexing, slicing -- array[행,열], array[:,:]
arr6 = np.array([[2,4,1], [6,7,8]]) #array생성 np.array([[0행초기값],[1행초기값],[2행초기값],....])
print(arr6[1, 2]) # 1행, 2열  -- index 는 0 부터 시작 --> 8 리턴
# boolean으로 slicing을 하면 slicing을 하는 행과 열의 shape에 맞춰서 넣어줘야함.
barr1 = np.array([[True,False,True,], [False,False,True]]) # 2차원 array생성
print(arr6)
#[[2 4 1]
# [6 7 8]]
print(barr1)
#[[ True False  True]
# [False False  True]]
print(arr6[barr1]) # [2 1 8] , boolean요소를 가진 ndArray로 slicing한다.
barr2 = np.array([False, True]) # 1차원 array생성
print(barr2) # [False  True]
print(arr6[barr2]) # [[6 7 8]]  2번째 행만 가져옴. print(arr6[barr2,:]) 과 동일
barr3 = np.array([True, False, True]) # 1차원 array생성
print(barr3) #[ True False  True]
print(arr6[:, barr3]) # 열(column)에 1차원 boolean형의 1차원 ndarray를 필터로 넣어줌.
#[[2 1]
# [6 8]]

## array 연산
arr1 = np.array([[1,2,3],[4,5,6]])
arr2 = np.array([[7,3,1],[8,2,3]])
print(arr1)
print(arr2)
print(arr1 + arr2)
print(arr1 * 3)
print(arr1 > arr2) #비교는 boolean으로 리턴
print(arr2 > 5)
print(arr1[arr1 >= 3])
print('##-------------------------------------------------')
# np.where() 는 첫번째 조건의 결과로 조건에 해당하는 index를 리턴함.
# 조건에 맞는 인덱스에는 2번째 인자의 값을 넣고, 아닌 곳에는 세번째 인자에서 지정한 값을 넣는다.
np.where(arr1 > 3, arr1, 0) # 조건문 arr1에서 3보다 큰거는 그대로, 같거나 작으면 0으로 채운다., 전체 배열에서 각각의 항목을 비교해서 3보다 크면 그대로, 아니면 0으로 
np.where(arr2 > 5, arr2 * 2, arr1) # arr2가 10보다 크면 2배, 그렇지 않으면 arr1의 해당 위치 값으로 설정
c = np.arange(5, 15) # array([ 5,  6,  7,  8,  9, 10, 11, 12, 13, 14])
print(c)
print(np.where(c % 3 == 0)) # 1, 4, 7번 위치가 6, 9, 12로 만족 -> (array([1, 4, 7]),) 값이 아닌 인덱스값을 리턴
print(np.where(c > 10)) # 6 ~ 9번 위치가 만족 -> (array([6, 7, 8, 9]),) 값이 아닌 인덱스값을 리턴.
d = np.array([[15, 8, 12], [11, 7, 3]])
print(d)
print(np.where(d > 10))
# 다소 결과가 복잡해보이는데, 2차원 이상이면 axis를 기준으로 인덱스 번호를 가져오게 됩니다.
# (array([0, 0, 1]), array([0, 2, 0]))를 해석해보면, 앞의 array는 axis = 0, 뒤의 array는 axis = 1에 해당하고,
# (0, 0), (0, 2), (1, 0)의 자리가 실제로 각각 15, 12, 11의 값이었으므로, 10보다 크다는 조건과 매칭된다는 점을 알 수 있습니다.
# (array([0, 0, 1]), array([0, 2, 0])) --> (값의 행 인덱스 모음, 값의 열 인덱스 모음)


## numpy 함수
e = np.array([[1,2,3],[4,5,6]])
print(np.sqrt(e)) 
print(np.exp(e))
print(np.sin(e))

arr8 = np.arange(8)
print(arr8)
print(np.mean(arr8), np.median(arr8), np.var(arr8), np.std(arr8))
rarr = arr8.reshape(4,2)    # 4행 2열
print(rarr)
trrar = rarr.T              # 행->열, 열->행
print(trrar)

print('##data-trrar-')
print(trrar)
print(f'mean,axis=0 : {np.mean(trrar, axis=0)}')   #해당 열(행을가로질러) 평균
print(f'mean,axis=1 : {np.mean(trrar, axis=1)}')   #해당 행(열을가로질러) 평균
print('##1-cumsum-cumprod--------------------------------------------------------')
print(f'cumsum,axis=0 : {np.cumsum(trrar, axis=0)}') #열 누적합
print(f'cumprod,axis=0 : {np.cumprod(trrar, axis=0)}')#열 누적곱
print('##2-----------------------------------------------------------------------')
print(f'cumsum,axis=1 : {np.cumsum(trrar, axis=1)}') #행 누적합
print(f'cumprod,axis=1 : {np.cumprod(trrar, axis=1)}')#행 누적곱
print('##data-rarr-')
print(rarr)
print('##1-----------------------------------------------------------------------')
print(np.cumsum(rarr, axis=0))  #열 누적합
print(np.cumprod(rarr, axis=0)) #열 누적곱
print('##2-----------------------------------------------------------------------')
print(np.cumsum(rarr, axis=1))  #행 누적합
print(np.cumprod(rarr, axis=1)) #행 누적곱

np.random.seed(111)
print(np.random.randint(low=1, high=10, size=(10, 2))) #size=shape..()되고, []된다
print(np.random.randn(5,2)) # 표준정규분포에서 5행2열 크기의 데이터를 뽑음, 크기를 지정하지 않으면 float의 단일값 출력
print(np.random.normal(loc=10, scale=5, size=[5,3])) # loc=평균, scale=표준편차, 평균10, 표준편자5 인 정규분포에서 값을 크기만큼 뽑음
```
