---
layout: post
title: ML6::Neural Networks:Learning
category: [Machine Learning]
tag: [Machine Learning, Neural Networks, backprogagation, Cost Fucntion]
description: 신경망 알고리즘은 가장 좋은 학습알고리즘 중 하나이다. 이번 포스팅에서는 주어진 데이터와 변수에 대해 알고리즘을 적용하는 방법을 알아보자.
---

신경망 알고리즘은 가장 좋은 학습알고리즘 중 하나이다. 이번 포스팅에서는 주어진 데이터와 변수에 대해 알고리즘을 적용하는 방법을 알아보자.


## Cost Function

![예1](/assets/posts/MachineLearning/ml5-0.png)

우선 신경망 알고리즘에서 사용하는 몇가지 변수의 정의를 짚고 넘어가자.

 - \\(L\\) : 신경망을 이루고 있는 **층(layer)**의 총 갯수<br>
 - \\(S_l\\) : l번째 층에 속해잇는 **개체(unit)**의 갯수 (bias unit은 포함하지 않는다.) 마지막 층은 L로 표시한다.<br>
 - \\(K\\) : **출력**으로 나타나는 개체(units)/클래스(classes)들의 수<br>
 
 위 그림에서는 L이 4 s1 = 3, s2 = 5, s2와s4 는 4가 된다. 분류(classification)문제를 풀기위해 신경망 알고리즘을 사용했다고 가정하면
 
이진 분류 (binary classification)에서는 결과가 하나(0 아니면 1)로 나타나므로 \\(S_L\\)은 1이 되고<br>
다중분류(Multi-class classification (K classes))에서는 \\(S_L\\) 은 K가 된다. <br>(여기서 K는 3보다 크다.)

신경망에서 사용하는 **비용함수(cost function)**은 Logistic regression에서 사용했던 비용함수를 변환한것이다. 이전 포스팅 Regularization에서 배웠듯이 Regularized logistic regression에서 사용한 비용함수는 아래와 같다.

<div>
$
J(\theta)=-\frac{{1}}{m}\sum_{i=1}^{m}\left[
 y^{(i)}\log(h_{\theta}(x^{(i)}))+
 (1-y^{(i)})\log(1-h_{\theta}(x^{(i)}))\right] + 
\frac{\lambda}{2m}\sum_{j=1}^{n}\theta_{j}^{2}
$
</div>


위 식에서는 하나의 유닛에 대한 cost function이지만 신경망의 경우 출력 유닛이 k개이므로 이에 맞게 식을 변경해야한다.


<div>
\begin{align*}
J(\Theta) = - \frac{1}{m} \left[ \sum_{i=1}^m \sum_{k=1}^K y^{(i)}_k \log ((h_\Theta (x^{(i)}))_k) + (1 - y^{(i)}_k)\log (1 - (h_\Theta(x^{(i)}))_k)\right] \newline +\frac{\lambda}{2m}\sum_{l=1}^{L-1} \sum_{i=1}^{s_l} \sum_{j=1}^{s_{l+1}} ( \Theta_{j,i}^{(l)})^2
\end{align*}
</div>

시그마가 몇개 더 붙었는데 굉장히 복잡해 보인다... 

인공신경망의 결과로나오는 여러 출력노드 k를 포현하위해 몇가지 시그마 연산을 했다. 식의 첫번째 부분 대괄호안의 시그마 연산이 층과 층사이에 거지물로 연결된듯한 연산을 표현한 것이다.

두번째항은 Regularization항이다. logistic regression의 regularization항과 비고해보면 엄청 복잡해진것 처럼 보이지만 theta matrix의 원소들을 곱한 값을 더하기 위해서 쓴 표현이다. 


## Backpropagation Algorithm


그렇다면 비용함수의 결과를 최소화하기 위해서는 어떻게 해야할까? Linear regression에서 처럼 gradient descent 알고리즘을 적용했듯이 신경망알고리즘의 비용함수를 최소화하기 위해서는 [**Backpropagation Algorithm**](https://en.wikipedia.org/wiki/Backpropagation)을 사용한다.

이 알고리즘의 목표는 \\(\min_\Theta J(\Theta)\\) 비용함수를 최소화하는 것 이다.

이를 위해서는 \\(J(\Theta)\\)와 
\\(\dfrac{\partial}{\partial \Theta_{i,j}^{(l)}}J(\Theta)\\)를 계산해야한다.

![예1](/assets/posts/MachineLearning/ml5-0.png)

이전 포스팅에서 **activation values**를  Forward propagation을 통해 계산하였다. 위에서 언급한 미분항을 계산하기 위해서 Backpropagation Algorithm을 사용한다.

---

## reference

 - [wikipedia - backprogagation algorithm](https://en.wikipedia.org/wiki/Backpropagation)