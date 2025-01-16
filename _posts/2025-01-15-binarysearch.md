---
layout: single
title: "개념 - 이진탐색"
author_profile: true
tags: [BinarySearch]
typora-root-url: ../
---
# Binary Search (이진탐색)

- 정렬되어있는 리스트에서 탐색 범위를 좁혀가며 데이터를 탐색함
- O(logN)
- 코드

```python
def binary_search(arr, value, start, end):

    if start > end: # 끝까지 못 찾았을 때
        return -1

    mid = (start + end) // 2

    if arr[mid] == value:
        return mid
    elif arr[mid] > value:
        binary_search(arr, value, start, mid-1)
    elif arr[mid] < value:
        binary_search(arr, value, mid+1, end)
```

- bisect_left(array, value), bisect_right(array, value)를 이용해서 가장 왼편, 오른편에 있는 찾고자 하는 수를 탐색 가능
  - from bisect import bisect_left
