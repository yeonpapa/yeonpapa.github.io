---
title: Airflow - airflow test
date: 2024-02-16 14:00:00 +0900
categories: [Data Analysis and Python Libs, Data Engineering]
tags: [airflow, workflow, dag, task]     # TAG names should always be lowercase
--- 

1. 조회<br>
* dag 조회
```$ airflow dags list```<br>
* task 조회 - airflow tasks list [dag_id]<br>
```$ airflow tasks list templates_test```<br>
```$ airflow tasks list templates_test --tree```<br>

2. dag 테스트<br>
* dag 테스트 - airflow dags test [DAG_ID] [EXECUTION_DATE] <br>
```$ airflow dags test helloworld_dag 2022-05-31```<br>
* task 테스트 - airflow tasks test [DAG_ID] [TASK_ID] [EXECUTION_DATE] <br>
```$ airflow tasks test helloworld_dag hello_world_task 2022-05-31```<br>


