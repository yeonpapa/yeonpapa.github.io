---
title: matplotlib - basic concept
date: 2023-06-07 22:00:00 +0900
categories: [Data Analysis and Python Libs, Data Visualization]
tags: [matplotlib, terms, graph]     # TAG names should always be lowercase
--- 

1. Basic
> import **matplotlib.pyplot** as **plt**
<br> plt.plot()함수는 함수에 하나의 **숫자리스트**를 입력함으로써 그래프가 구성됨. 
<br> (예1) plt.plot([1,2,3,4]) 하나의 리스트가 입력되면 Y값으로 판단하고, 자동으로 X를 1,2,3,4로 할당
<br> (예2) plt.plot([1,2,3,4],[1,4,9,16])
<br> (예3) data_dict={'x':[1,2,3], 'y':[2,3,5]} , plt.plot('x', 'y', data=data_dict)
<br> plt.show() 함수를 통해 그림이 나타남.

2. 포맷스트링, 축, 축범위, 축레이블, 범례
> - 포맷스트링 : plt.plot([1, 2, 3, 4], [1, 4, 9, 16], 'ro') 'ro' : red색상, ㅇ:원모양 
- 축 범위 지정1: plt.axis([xmin,xmax,ymin,ymax]) : x축, y축의 범위를 지정
- 축 범위 지정2: plt.xlim(xmin, xmax), plt.ylim(ymin, ymax)
축 axis()의 option : plt.axis('sqare') : options - 'on' | 'off' | 'equal' | 'scaled' | 'tight' | 'auto' | 'normal' | 'image' | 'square'
- plt.xlabel('X-Axis',labelpad=15, fontdict={'family':'serif','color':'b','weight':'bold','size':14}), plt.ylabel('Y-Axis')
- plt.plot([1, 2, 3, 4], [2, 3, 5, 10], label='Price ($)')처럼, label설정하고, plt.legend(loc='lower right') 호출
- xticks, yticks 는 눈금을 뜻함, 눈금의 값도 label로 바꿀수 있음.범주형일 경우 유용함--> xticklabels('A','B')

3. subplot, figure, axes
> - subplot은 여러개의 그래프를 그림 plt.subplot(row, column, index)
- figure 는 전체 도화지, axes는 전체 도화지 안에 들어가는 그래프들
```
fig = plt.figure(figsize=(12, 8))
ax = fig.add_subplot(1, 1, 1)
ax.plot(x, y)
## setting xticks, yticks with labels
ax.set_xticks([0, 50, 100])
ax.set_yticks([-2, 0, 2])
ax.set_xticklabels(['start', 'middel', 'end'], fontsize=12)
ax.set_yticklabels(['low', 'zero', 'high'], fontsize=12)
## xlabel, ylabel
ax.set_xlabel('Steps', fontsize=16)
ax.set_ylabel('Value', fontsize=16)
# title
ax.set_title('Plo with ticks and labels', fontsize=20, loc='left') # 'center', 'right'
plt.show()
```