---
title : " Two Pointers "
describe : " python array algorithm "

categories:
  - algorithm
tags:
  - python
  - algorithm
use_math: true
comments: true
last_modified_at : 2021-03-05-10:49
---

### 투포인터 기법이란?
---
 두 개의 포인터를 이용해 순차적으로 접근하면서 포인터 간 데이터가 원하는 데이터가 될때까지 포인터를 조작하는 기법을 의미한다. 쉽게 말하면 시작점과 끝점을 기준으로 문제를 풀어나가는 전략을 말한다. 일반적으로 배열이 정렬되어있을 때 유용한 측면이 있다.   


 예를들어 어떤 배열(a)에서 조건값(s)을 만족하는 숫자쌍을 리턴하는 함수를 구현하라는 문제가 주어졌을때 가장 일반적이고 원초적인 풀이법은 다음과 같다. 

> a = [1,6,7,8,2,3,4,9,5]  
> s = 12

### brute force
``` python
def solution(a, s):
    answer = []
    for i in range(len(a)):
        for j in range(i+1, len(a)):
            if a[i] + a[j] == s:
                answer.append([a[i],a[j]])
    return answer

print(solution(a, s))
```

코드에서 살펴볼 수 있듯, 예제의 풀이에서 2중 for문을 사용할 경우 시간복잡도가 $O(n^2)$ 소모된다. 다음은 Two Pointers를 이용한 해결법이다. 


### Two Pointers
``` python
def solution_two_pointers(a,s):
    # 정답을 담을 리스트
    answer = []

    # 배열 정렬
    a.sort()
    
    # 좌우측 포인터 설정
    left, right = 0, len(a)-1

    while left <= right:
        check = a[left] + a[right]
        if check > s: # 조건 불만족 포인터 이동
            right -= 1
        elif check < s: # 조건 불만족 포인터 이동
            left += 1
        else: # 조건을 만족하였으므로 정답 리스트에 담기
            if left == right:
                break
            answer.append([a[left],a[right]])
            left += 1 # 다음 탐색을 위한 포인터 이동 
            right -= 1

    return answer
```

배열을 정렬한 뒤 left 포인터와 right 포인터가 만날때까지 반복한다. 배열을 한번만 탐색하기 때문에, 정렬된 배열의 경우 $O(n)$으로 해결이 가능하며 정렬이 되어있지않더라도 $$O(n\log{}n)$$로 해결이 가능하다. 

이렇듯 Two Pointers는 주로 정렬된 배열을 대상으로 하며 두 개의 포인터가 좌우로 자유롭게 움직이며 문제를 해결한다. Sliding Window와 비슷한 점이 많은 풀이법이다. 

