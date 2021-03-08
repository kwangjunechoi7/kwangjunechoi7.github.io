---
layout: article
title: Python Metaprogramming Part_A

aside:
 toc: true

categories:
  - programming

tags: 
    - python
    - programming
use_math: true
comments: true
last_modified_at : 2021-03-08-21:00
---

# Define Metaprogramming in python
메타프로그래밍 의 사전적 정의는 자기 자신 혹은 다른 컴퓨터 프로그램을 데이터로 취급하며 프로그램을 작성, 수정하는 것을 말한다. <sup>[1](#footnote_1)</sup> 소프트웨어 개발에서는 반복적으로 되풀이 되는 코드를 작성할 때는 대개 그보다 현명한 해결책이 존재한다. Python에서는 이러한 문제를 메타프로그래밍이라는 카테고리로 분류한다. <sup>[2](#footnote_2)</sup> 수정, 생성, 기존 코드 감싸기 등 코드를 다루는 함수나 클래스를 만들거나 커스터마이징하는 행위를 의미하는 것이다. 이를 통해 특정 클래스의 동작을 제어할 수 있다. 주요 기능으로 데코레이터, 클래스 데코레이터가 있다. 그외에도 signiture object, exec()로 코드 실행이나 클래스와 함수 내부 조사등 유용한 기능도 가능하다. 허나 대부분의 파이썬 프로그래밍은 메타클래스를 사용하지 않고 구현이 가능하다. 

## Function을 감싸는 wrapper
function에 타이밍과 같이 추가적인 처리를 하는 wrapper layer를 넣어본다. 함수에 추가적인 코드를 감싸려면 아래와 같이 데코레이터 함수를 정의한다. 

``` python
import time 
from functools import wraps

def timethis(func):
    """
    실행 시간을 보고 하는 데코레이터
    """
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(func.__name__, end-start)
        return result

    return wrapper

# 데코레이터는 입력으로 함수를 받고 새로운 함수를 반환함
# @staticmethod, @classmethod, @property와 같이 내장된 데코레이터도 동일하게 동작함 
@timethis
def countdown(n):
    """
    counts down 
    """
    while n > 0:
        n -= 1

countdown(100000)
# countdown 0.013844966888427734
``` 
본래 원본 입력 함수를 호출하고 별과를 반환한다. 추가적인 타이밍 코드를 통해 wrapper가 결과로 반환되었고 원본 함수를 대신했다. 새로 생성한 데코레이터는 일반적으로 호출 시그니처나 감싸고 있는 함수의 반환값을 수정하지 않는다. 그리고 어떠한 입력인자도 받을 수 있도록 *args, **kwargs가 사용되었다. 




### Reference
__________________________________________________________________
<!-- 글 뒷 부분에 -->
<a name="footnote_1">1</a> : [출처_위키백과 메타프로그래밍](https://ko.wikipedia.org/wiki/%EB%A9%94%ED%83%80%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)  
<a name="footnote_2">2</a> : Python Cookbook