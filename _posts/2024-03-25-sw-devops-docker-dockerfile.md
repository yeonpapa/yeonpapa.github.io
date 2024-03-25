---
title: (DOCKER) Dockerfile, docker-compose
date: 2024-03-25 09:00:00:00 +0900
categories: [SW DevOps, Container]
tags: [swdevops, docker, dockerfile, docker-compose]     # TAG names should always be lowercase
--- 

## Dockerfile
Docker image를 만들기 위한 파일. 문서로서 이미지를 생성하고 실행(컨테이너)함.

``` Dockerfile
FROM python:3.9
COPY requirements.txt app/requirements.txt
WORKDIR /app
RUN pip install -r requirements.txt
COPY . /app
EXPOSE 8501
CMD ["streamlit", "run", "echart_demo.py"]
```

## docker-compose
- 하나의 문서에 여러 개의 컨테이너를 정의<br>
- Docker Compose는 다중 컨테이너 애플리케이션을 정의 공유할 수 있도록 개발된 도구로 단일 명령을 사용하여 모두 실행 또는 종료할 수 있도록 개발된 도구

```yaml
version: '3'  # docker-compose file format의 버전
services:
  streamlit_app:
    build: .     #현재 디렉토리에서 Dockerfile을 찾아서 빌드
    volumes:
      - .:/app
    ports:
      - 8501:8501
```

