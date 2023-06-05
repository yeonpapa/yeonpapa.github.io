---
title: Jupyter Notebook - 한글깨짐 및 음수표현
date: 2023-06-05 10:00:00 +0900
categories: [Data Analysis and Python Libs, etc]
tags: [jupyternotebook]     # TAG names should always be lowercase
--- 

##### Jupyter Notebook
1. 한글 깨짐 현상과 음수(-) 표시
> C:\Users\[사용자id]\AppData\Local\Programs\Python\Python310\Lib\site-packages\matplotlib\mpl-data\matplotlibrc
<br> 아래 설정 주석 해제( # 표시삭제)
<br> font.family:  Malgun Gothic ## 원하는 폰트 설정 
<br> axes.unicode_minus: False   ## False 로 설정해야 그래프에서 음수(-) 표시됨