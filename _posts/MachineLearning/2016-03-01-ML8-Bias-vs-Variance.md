---
layout: post
title: 8.Bias vs. Variance
category: [ML]
tag: [Machine Learning, undercutting, overfitting, bias, varriance]
description: 이번 포스팅에서는 bias와 varriance에 대해서 깊게 알아보고 알고리즘이 bias문제가 있는지 varriance문제가 있는지 평가하는 방법에 대해서 알아본다. 그리고 이경우 어떻게 알고리즘을 향상시킬수 있는지 알아본다.

---

우리가 생각한대로 머신러닝 알고리즘이 정확히 작동하면 좋겠지만 거의 모든경우에 **High Bias**혹은 **High Variance** 문제가 발생한다. (다른 말로 undercutting problem, overfitting problem) 이 경우에 어떤 문제를 가지고 있는지 알아내는것이 중요하다. 그렇게 해야만 알고리즘을 더 좋은 방향으로 수정할 수 있기 때문이다.

이번 포스팅에서는 bias와 varriance에 대해서 깊게 알아보고 알고리즘이 bias문제가 있는지 varriance문제가 있는지 평가하는 방법에 대해서 알아본다. 그리고 이경우 어떻게 알고리즘을 향상시킬수 있는지 알아본다.

# Diagnosing Bias vs. Variance

polynomial degree **d**에 대한 **underfitting**과 **overfitting**의 관계를 알아보자.

![예1](/images/MachineLearning/ml8/0.png)

왼쪽 그림부터 polynomial degree는 각각  1,2,4이다. 가장 왼쪽 표현은 High bias(underfit)문제가 있고 오른쪽은 High variance(overfit)문제가 있다. 이번 포스팅에서 알아본대로 cross validation set을 이용해서 테스트를 하면 가장 적절한 polynomial model은 degree가 2인 모델임을 알 수 있다.

알그리즘이 잘 작동하지 않는 경우는 **cross validation error**가 크거나 **test error**가 클때이다. 다음 그림을 살펴보자.

![예1](/images/MachineLearning/ml8/300px-Features-and-polynom-degree.png)

polynomial degree에 따른 error를 그래프로 나타내보자. 

 - 빨간선(training error)
 - 초록선(cross validation error)

보통 training error는 d가 커질수록 줄어드는 경향이 있다. 그리고 동시에 


---

## reference 

 - [Machine learning by Andrew Ng](https://www.coursera.org/learn/machine-learning)
 - [Lec38. Machine Learning(머신러닝) ? Evaluating a Learning Algorithm and Cross Validation(교차 검증) 작성자 헐멍](http://blog.naver.com/mypa3424/220576318791)
 

