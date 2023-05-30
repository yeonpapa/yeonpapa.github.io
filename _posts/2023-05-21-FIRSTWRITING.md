---
title: 분포의 이해
date: 2023-05-21 14:22:00 +0900
categories: [Data Analysis and Python Libs, Basic Statistics]
tags: [statistics, probability, pdf, pmf]     # TAG names should always be lowercase
--- 

###### 확률분포(probability distribution)은 __확률변수__ 가 특정한 값을 가질 __확률__ 을 나타내는 함수를 의미한다. 확률변수가 특정 값을 가질 확률이 얼마나 되느냐를 나타내는 것입니다. 확률분포는 확률변수의 종류에 따라 __이산확률분포__ 와 __연속확률분포__ 로 나뉘는데요. 쉽게 말해 확률변수를 셀 수 있는지 없는지에 따라 나눈다고 생각하시면 됩니다.

1. 연속형 확률분표
>  확률변수 X를 대한민국 성인 남성 평균 키라고 했을 때, X는 키(cm)로 실수값을 가지며 이는 ‘셀 수 없는’ 경우에 해당합니다. x:확률변수, p(x>=170):170 이상인 확률, 구간으로 나타냄
   * 확률 밀도 함수(probability density function, pdf)
   * 종류

2. 이산형 확률분포
> 확률변수 X를 주사위를 던져서 나오는 눈의 개수라고 하면 X는 1,2,3,4,5,6 여섯가지 경우를 가질 수 있습니다. x:확률변수, p(x=1): 1이 나올 확률
   * 확률 질량 함수(probatility mass function, pmf)
   <!-- <img src="_posts/img/Fair_dice_probability_distribution.jpg" width="450px" height="300px" title="pmf" alt="pmf"></img><br/> -->
   * 종류

