---
title: (PYTHON) PYTHON LIBRARY 설치 방법
date: 2023-08-24 13:00:00:00 +0900
categories: [SW Development, Backend]
tags: [swdev, python, pip, install, download]     # TAG names should always be lowercase
--- 

### PYTHON Library 설치 방법
1. On-line인 경우
> ```
  pip install {package이름==version}
  pip list
  pip freeze > requirements.txt
  pip install -r requirements.txt
  ```

2. Off-line인 경우
> On-line인 PC에서 download 받아서 off-line PC로 옮겨서 설치<br/>
- d : destination folder<br/>
- no-index : package index무시하고 오직 find-links에서 지정한 폴더에서 찾아서 설치<br/>
- find-links : downloaded python package가 있는 폴더<br/>
```
pip download -d ./packages -r requirements.txt
pip install --no-index --find-links=./packages/ -r requirements.txt
```

