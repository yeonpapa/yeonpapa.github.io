---
title: (PYTHON) 자료구조, 알고리즘 - 1
date: 2024-05-11 16:00:00:00 +0900
categories: [SW Development, Programming Language]
tags: [swdev, python, data-structure, algorithm]     # TAG names should always be lowercase
--- 

### 자료구조
1. Array : list
2. Linked List : python으로 직접구현은 굳이 할 필요없음list사용. but 면접시, 직접구현 요청시, Node 클래스 정의 및 method구현 
3. Stack : deque
4. Queue : deque
   - 큐(deque)
   - 우선순위큐(heapq)
5. Graph : dict와 list/dict를 활용하여 graph자료구조 표현 - dict(Key:노드명, Value:이웃노드들(list))
6. Hash table : key에 데이터를 저장하는 구조로서 파이썬에서는 dict 사용하면 됨
   - hash키 : data를 고정된 길이로 변환(key 생성) ex. dictionary의 key에 해당하는 data를 가지고 일정길이의 숫자 형태의 key생성<br>
              hash(), hashlib - sha1(), sha256()
   - hash함수 : hash key를 입력 받아서 데이터가 저장되어있는 hash주소를 return, 주소가 동일할 수 있다. 예를 들어 key를 나눈 나머지인 경우
   - hash collision 해결 : chaining(open hashing), linear probing(close hashing) 기법
7. Tree : 노드와 브랜치로 구성된 Cycle이 존재하지 않는 자료구조, 탐색에 유리
   - Binary Tree : 노드가 가지는 최대 브랜치의 수가 2개인 트리
   - Binary Search Tree : 특정 노드의 왼쪽 편 노드가 오른쪽 노드 보다 작은 값이 오게 만들어 놓은 Tree
8. Heap : 완전이진트리(complete binary tree) 기반: 노드를 삽입시 최하단 왼쪽 노드부터 차례로 삽입하는 Tree, 최대값, 최소값을 찾을떄 유리
   - 최대힙(루트노드가 가장 큰값), 최소힙(루트노드가 가장작은값)

### 알고리즘
1. Sort(정렬) : *list*.sort(), sorted(*list*)
   - 단순(bubble, selection) : O(n<sup>2</sup>)
   - 파이썬 정렬 함수 : O(nlogn)

2. Search(탐색)
   - 순차
   - 이진 : bisect

3. 그래프(노드)탐색-I : 
   - BFS(Breadth-First Search) : 정점과 같은 레벨에 있는 노드(형제)들을 먼저 탐색, Graph와 Queue 2개 활용(visited, need_visit) : O(V(노드수) + E(간선수))
   - DFS(Depth-First Search) : 정점의 자식을 먼저 탐색,  Graph와 Queue(visited), Stack 활용(need_visit) : O(V(노드수) + E(간선수))

4. 최단 경로 알고리즘 : 그래프탐색-II (가중치그래프)
   - 다익스트라 (단일 출발 최단 경로 문제) ,그래프는 dict안의 dict로 우선순위 큐를 사용

5. 최소 신장 트리 알고리즘(Minimum Spanning Tree)
   - 크루스칼 알고리즘(Kruskal's algorithm) - Key concept:greedy algorithm, union-find 알고리즘(union-by-rank), path compression
   - 프림 알고리즘(Prim's algorithm) - heapq, defaultdict
   - 개선 프림 - heapdict

### 전략
1. 탐욕 (greedy) : 매 순간 최적이라고 생각되는 경우를 선택하여 수행 --> 전체 최적의 방법은 아님, 최적근사치를 구함(한계)
   - 동전 문제
   - 부분 배낭 문제 
2. Backtracking 
   - N Queen
3. Divide conquer
4. Recursive
5. 동적계획법
