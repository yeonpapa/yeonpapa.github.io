---
title: (PYTHON) 자료구조, 알고리즘 - 1
date: 2024-05-11 16:00:00:00 +0900
categories: [SW Development, Programming Language]
tags: [swdev, python, data-structure, algorithm]     # TAG names should always be lowercase
--- 

### 자료구조
1. Stack : deque
2. Queue : deque
   - 큐(deque)
   - 우선순위큐(heapq)
3. Graph : dict와 list/dict를 활용하여 graph자료구조 표현 - dict(Key:노드명, Value:이웃노드들(list))
4. Hash table
5. Tree : cycle이 존재하지 않는 Graph
   - Tree
   - Binary Search Tree
6. Heap

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
