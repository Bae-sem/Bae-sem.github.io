---
layout: single
title: "개념 - 우선순위 큐"
author_profile: true
tags: [Priority Queue]
typora-root-url: ../
---
# Priority Queue (우선순위 큐)

- 우선순위가 가장 높은 데이터를 가장 먼저 삭제하는 자료구조
  - 예를 들어 여러 개 물건 데이터 자료구조를 넣었다가 가치가 높은 물건 데이터 부터 꺼내서 확인해야 하는 경우

| 자료구조                     | 추출되는 데이터             |
| ---------------------------- | --------------------------- |
| Stack (스택)                 | 가장 나중에 삽입된 데이터   |
| Queue (큐)                   | 가장 먼저 삽입된 데이터     |
| Priority Queue (우선순위 큐) | 가장 우선순위가 높은 데이터 |

- 최소 힙: 값이 낮은 데이터 부터 추출되는 형식
- 최대 힙: 값이 높은 데이터 부터 추출되는 방식

| 우선순위 큐 구현 방식 | 삽입 시간 | 삭제 시간 |
| --------------------- | --------- | --------- |
| 리스트                | O(1)      | O(N)      |
| 힙 (Heap)             | O(logN)   | O(logN)   |

- 트리 구조로 삽입과 삭제를 다루기 때문에, 삽입과 삭제 둘다 O(logN)의 시간이 걸리게 된다

```python
import heapq # 우선순위 큐 라이브러리

array = []

heapq.heappush(array, value) # 우선순위 큐 삽입
heapq.heappop(array) # 우선순위 큐 출력
```

```python
import heapq

# 오름차순 힙 정렬 (Heap Sort) - 최소 힙
def heapsort(iterable):
	h = []
	result = []
	# 모든 원소를 차례대로 힙에 삽입
	for value in iterable:
		heapq.heappush(h, value)
	# 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
	for i in range(len(h)):
		result.append(heapq.heappop(h))
	return result

result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 9])
print(result)

# 내림차순 힙 정렬 - 최대 힙
def heapsort(iterable):
	h = []
	result = []
	for value in iterable:
		heapq.heappush(h, -value)
	for i in range(len(h)):
		result.append(-heapq.heappop(h))
	return result
```