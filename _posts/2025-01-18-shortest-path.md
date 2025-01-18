---
layout: single
title: "개념 - 최단경로"
author_profile: true
tags: [Shortest Path]
typora-root-url: ../
---
# 최단 경로 알고리즘

- 가장 짧은 경로를 찾는 알고리즘을 의미한**다**
- **다양한 문제 상황**
    1. 한 지점에서 다른 한 지점까지 최단 경로
    2. 한 지점에서 다른 모든 지점까지 최단 경로
    3. 모든 지점에서 다른 모든 지점까지 최단 경로

---

# 1. 다익스트라 최단 경로 알고리즘

- 2번 문제 상황 (한 지점에서 다른 모든 지점까지 최단 경로)
- 간선에 음의 값이 없을때에 사용 가능
- 시간 복잡도: O(ElogV)  #E = 간선, V = 노드
- 동작과정
    1. 출발 노드를 설정한다
    2. 최단 거리 테이블을 초기화 한다 (다른 노드에 대한 거리를 무한으로 설정)
    3. 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택한다
    4. 해당 노드를 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신한다
    5. 위 과정에서 3번과 4번을 반복한다
- 특징
    - 그리디 알고리즘: 매 상황에서 방문하지 않은 가장 비용이 적은 노드를 선택해 과정을 반복한다
    - 단계를 거치면 한 번 처리된 노드의 최단 거리는 고정되어 더 이상 바뀌지 않는다 (한 단계당 하나의 노드에 대한 최단 거리를 확실히 찾는 방식)

```python
import sys
import heapq
input = sys.stdin.readline
INF = int(1e9) #무한

n. m = map(int, input().split()) # 노드, 간선 개수
start = int(input()) # 시작 노드 번호
graph = [[] for i in range(n + 1)] # 각 노드 연결되어 있는 노드 정보 담는 리스트 선언
distance = [INF] * (n + 1) # 최단 거리 테이블을 모두 무한으로 초기화

# 모든 간선 정보 입력 받기
for _ in range(m):
	a, b, c = map(int, input().split()) # a 노드 에서 b 노드 까지 가는 비용이 c 이다
	graph[a].append((b, c))
	
def dijkstra(start):
	q = []
	heapq.heappush(q, (0, start))	
	distance[start] = 0 # 시작 위치 거리 초기화
	while q:
		dist, now = heapq.heappop(q)
		if distance[now] < dist:
			continue
		for i in graph[now]:
			cost = dist + i[1]
			if cost < distance[i[0]]:
				distance[i[0]] = cost
				heapq.heappush(1, (cost, i[0]))
			
dijkstra(start) # 알고리즘 수행

#출력
for i in range(1, n + 1):
	if distance[i] == INF:
		print("X")
	else:
		print(distance[i])
```

---

# 2. 플로이드 워셜 알고리즘

- 3번 상황 (모든 노드에서 다른 모든 노드까지의 최단 경로를 모두 계산)
- 시간 복잡도: O(N^3) #적은 노드일때 사용
- 각 단계마다 특정한 노드 k를 거쳐 가는 경우를 확인한다
    - a에서 b로 가는 최단 거리보다 a에서 k를 거쳐 b로 가는 거리가 더 짧은지 검사하면 된다.
    - 점화식은 아래와 같다
    
    $$
    D_{ab} = min(D_{ab}, D_{ak} + D_{kb})
    $$
    
- 동작과정
    1. 초기: 그래프를 준비하고 최단 거리 테이블을 초기화 한다 
    
    $$
    D_{ab} = min(D_{ab}, D_{ak} + D_{kb})
    $$
    
    1. 1번 노드를 거쳐 가는 경우를 고려하여 테이블을 갱신 한다 
    
    $$
    D_{ab} = min(D_{ab}, D_{a1} + D_{1b})
    $$
    
    1. 2번과 같이 모든 노드 (2, 3, 4, …) 에 대하여 테이블을 갱신 한다

```python
INF = int(1e9)

n = int(input()) # 노드 개수
m = int(input()) # 간선 개수

graph = [[INF] * (n + 1) for _ in range(n + 1)] # 2차원 리스트를 무한으로 초기화

# 자기 자신에서 자기 자신으로 가는 비용은 0 으로 초기화
for a in range(1, n + 1):
	for b in range(1, n + 1):
		if a == b:
			graph[a][b] = 0

# 각 간선에 대한 정보를 입력 받아, 그 값으로 초기화
for _ in range(m):
	a, b, c = map(int, input().split()) # A에서 B로 가는 비용은 C라고 설정
	graph[a][b] = c

# 점화식에 따라 플로이드 워셜 알고리즘 수행
for k in range(1, n + 1):
	for a in range(1, n + 1):
		for b in range(1, n + 1):
			graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b]

#출력
for a in range(1, n + 1):
	for b in range(1, n + 1):
		if graph[a][b] == INF:
			print("X", end = " ")
		else:
			print(graph[a][b], end = " ")
	print()
```

---

# 3. 벨만 포드 알고리즘

- 음수 간선이 존재할때 사용
- 한 지점 → 한 지점 or 한 지점 → 모든 지점 일때 사용

### 작성 진행중…

---

## **특성에 따른 최단경로 알고리즘 선택**

1. 한 지점 → 한 지점

- 모든 간선의 가중치가 1로 동일: BFS (O(V+E))
- 간선마다 가중치가 다름, 음수 없음: 다익스트라 (O(E log V))
- 음수 가중치 존재: 벨만-포드 (O(VE))

2. 한 지점 → 모든 지점

- 모든 간선의 가중치가 1로 동일: BFS (O(V+E))
- 간선마다 가중치가 다름, 음수 없음: 다익스트라 (O(E log V))
- 음수 가중치 존재: 벨만-포드 (O(VE))

3. 모든 지점 → 모든 지점

- 모든 간선의 가중치가 1로 동일: 각 정점마다 BFS (O(V(V+E)))
- 간선마다 가중치가 다름:
    - 정점 수가 적을 때(<500): 플로이드-워셜 (O(V³))
    - 정점 수가 많을 때: 다익스트라 V번 (O(VE log V))
- 음수 가중치 존재: 플로이드-워셜 (O(V³))

* BFS/DFS 는 최단경로 라기 보다는, "몇 개의 간선을 거쳐 갔는가"를 기준으로 하는 알고리즘이다.