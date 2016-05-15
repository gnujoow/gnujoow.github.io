---
layout: post
title: dynamic programming
category: [ALGO]
tag: [Algorithm, Dynamic Programing, dp]
description: 다이나믹 프로그래밍에 대해서 알아보자.
---

DP 어렵다. DP잘 하고 싶어서 공부한 내용을 정리해본다.


# 다이나믹 프로그래밍

**작은 문제의 답을 조합해서 큰 문제의 답을 푼다.**

다이나믹 프로그래밍은 최적화 문제를 연구하는 수학 이론에서 왔다고 한다. Richard Bellman이란 사람이 이름이 멋있어서 붙였다고 한다. <del>이름이 멋있지만 이름 자체가 이름이 멋있어서 붙인거라고 한다.</del> 다이나믹은 아무런 의미가 없다. 따라서 **동적 계획법** 이 올바른 번역이라고 한다. <del>프로그램과 상관없음</del>


다이나믹 프로그래밍은 문제의 답이 이용되는 구조를 이용한 알고리즘이다. 큰 문제를 작은 문제로 나눈다는 측면에서 분할정복(divide and conquer)알고리즘과 비슷하지만 다음과 같은 차이점이 존재한다.

| DaC 						 | DP 					|
|------------------|-----------------|
| 문제가 절반으로 줄어듬 | 문제가 -1 로 줄어듬 |
| Function problem | 최적화 문제					|
| 결과가 한번 사용 		| 결과가 여러번 사용됨 	|
| 분할이 성능 향상 		| 결과 재사용이 성능 향상 |

다이나믹 프로그래밍 알고리즘을 적용하기 위해서는 아래와 같은 조건을 만족해야 한다.

- Overlapping Subproblem
- Optimal Substructure

**Overlapping Subproblem** 은 중복되는 부분 문제이다. 예를 들면 N번째 피보나치수를 구하는 문제를 구하는 문제는 N-1번째 N-2번째 피보나치 수를 구하는 문제가 되고 다른 수를 구할 때 같은 문제가 겹치는 경우가 생긴다.  
큰 문제와 작은 문제를 같은 방법으로 풀 수 있어야한다. 그리고 문제를 작은 문제로 나누어서 풀 수 있어야한다.

**Optimal Substructure** 문제의 정답을 작은 문제의 정답을 구할 수 있다.

다이나믹 프로그래밍에서는 작은 문제들을 한 번만 풀어야한다.(시간을 줄이려면 당연히) 그리고 정답을 구했으면 이 답을 어딘가 메모해놓고 (**Memoization**) 이 답들을 이용해서 큰 문제를 푼다. 그리고 저장되는 공간을 cache라고 한다. 따라서 DP를 구현하기 위해서는 메모를 작성하는 부분과 메모를 읽는 부분이 필요하다. 피보나치 수를 구하는 예제를 살펴보면서 DP를 더 자세히 알아보자.

{% highlight c %}
int fibonacci(int n){
	if (n <= 1) return n;
	else{
		return fibonacci(n-1) + fibonacci(n-2);
	}
}
{% endhighlight %}
> 스타트링크 다이나믹 프로그래밍 시작하기 동영상 (29:46)

피보나치 수열을 구하는 함수가 작동하면 함수의 재귀호출로 작은 피보나치수 들을 구하게 되는데 이때 중복해서 구해지는 수들이 있다. 이를태면 `fibonacci(2)`,`fibonacci(3)`이 여러번 호출된다.

{% highlight c %}
int memo[100]={0,};
int fibonacci(int n){
	if( n <= 1) return n;
	else{
		if(memo[n] > 0) return memo[n];
		memo[n] = fibonacci(n-1) + fibonacci(n-2);
		return memo[n];
	}
}
{% endhighlight %}
> 스타트링크 다이나믹 프로그래밍 시작하기 동영상 (33:10)

이렇게 작은 문제를 풀 때 작은 문제들의 답을 메모를 하고 중복되는 작은 문제를 풀어야 할 때는 이미 답을 알고 있으므로 메모된 답을 이용하면 더 빠르게 풀 수 있다.

---

다이나믹 프로그래밍 문제를 푸는 방법에는 크게 두가지가 있다.

- Top-down
- Bottom-Up

**Top down** 방식으로 문제를 푸는 방법은 다음과 같다.

1. 문제를 작은 문제로 나눈다.
2. 작은 문제들을 푼다.
3. 작은 문제들의 답으로 전체 문제를 푼다.

위의 피보나치 수열을 구하는 방법이 Top-down의 좋은 예이다. 주로 재귀함수를 이용해서 구현한다고 한다.

**Bottom-Up** 방식으로 문제를 푸는 방법은 다음과 같다.

1. 가장 작은 문제부터 푼다.
2. 문제의 크기를 점점 크게 만들어서 전체문제를 푼다.

---

# reference

- [다이나믹 프로그래밍 시작하기 - 스타트링크](https://www.youtube.com/embed/0o2hF-To_6Q)
- [프로그래밍대회에서 배우는 알고리즘 해결전략](http://book.algospot.com/) 1권 8장 동적 계획법
- [위키피디아:동적계획법](https://ko.wikipedia.org/wiki/%EB%8F%99%EC%A0%81_%EA%B3%84%ED%9A%8D%EB%B2%95)
- [wikipedia:dynamic Programing](https://en.wikipedia.org/wiki/Dynamic_programming)
