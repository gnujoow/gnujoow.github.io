---
layout: post
title: ML3::Logistic Regression
category: Machine Learning
---
## Classification and Representation

### Classification

이메일이 스펨인지 아닌지 온라인 매물이 허위매물인지 아닌지 구분하는 것 처럼 데이터를 어떤 기준에 의해 분류하는 문제를 분류문제(classification problem)이라고 한다. ML::0참고

그럼 Classification 알고리즘을 어떻게 만들까? 이전에 다루었던 종양 문제를 다시 살펴보자.

![](/assets/posts/MachineLearning/ml3-0.png)

종양 크기에 따라 악성종양인지 아닌지 구분하였다. 앞서 배운 Linear regression으로 모델을 표현하는 가설함수를 만들면 아마 빨간색 실선이 될 것이다. 이 문제에 대해서 예측을 하려고 한다면 가설함수의 y축이 0.5보다 크면 악성, 0.5보다 작으면 악성이 아님으로 기준을 잡을 수 있다.

![](/assets/posts/MachineLearning/ml3-1.png)

이 모델에 오른쪽에 파란색 화살표로 표시한 원소를 하나 추가 시키자. 딱히 이 모델이 바뀌진 않았지만 이 모델을 가장 잘 표현하기 위해 비용함수(cost function)의 값이 작아지는 쪽으로 가설함수가 만들어질 것이고 그렇다면 위의 파란색 실선처럼 가설함수를 표현할 수 있다. 앞에서 했던것과 같이 한계점(threshold)를 0.5로 잡으면 가설함수의 y축이 0.5가 되는 x의 좌표를 기준으로 데이터들을 분류(classify)할 수 있을것이다. 그렇게 된다면 경우에 따라, 특히 이 경우에는 잘못 분류되는 데이터들이 생기게 된다. 이 경우 linear regression을 적용했을때 나타나는 안좋은 경우 중 하나이다.

경우에 따라 운이 좋아서ㅋ linear regression이 모델을 잘 표현할 때도 있지만 보통은 그렇지 않으므로 Andrew Ng교수님은 classification문제에 linear regression을 사용하지 않는다고 하신다.

만약 classcification을 통해 y가 0 또는 1 로 분류하고 싶을 때 linear regression의 가설함수 h(x)는 0보다 작거나 1보다 큰 경우가 있어 적절하지 않다.

따라서 **가설함수(hypothesis function)**의 값이 0과 1사이인 **Logistic Regression**에 대해서 알아보도록 하자. Regression이란 이름이 나와서 당황스러울수도 있지만 Logistic Regression 알고리즘은 사실 classification문제에 사용하는 알고리즘 중 하나이다.

### Hypothesis Representation

그럼 **분류(classification)**문제에서 **가설함수(hypothesis function)**를 어떻게 표현하는지 알아보자. 

<div>
범위가 $0 \leq h_\theta (x) \leq 1$인 logistic model을 표현하는 가설함수는 $  h_\theta (x) =  g ( \theta^T x )$로 표현한다. 
<br><br>linear regression의 가설함수와 비교하면 $g()$가 $\theta^Tx$(linear regression의 가설함수)를 감싸고있는걸 알 수 있다.
</div>

\\(g(z) = \dfrac{1}{1 + e^{-z}} \\)는 **sigmoid function**혹은 **logistic function**이라고 한다.

![sigmoid function](/assets/posts/MachineLearning/ml3-2.png)

sigmoid function은 g(z)와 z축에 각각 1, 0에 점근선이 그려진다.

### Decision Boundary

그럼 분류문제에서 logistic function을 이용해서 어떻게 분류를 할까

0 혹은 1 분류에서 가설함수의 결과에 따라서 0, 1을 분류하면 된다.

<div>
$
\begin{align*}
& h_\theta(x) \geq 0.5 \rightarrow y = 1 \newline
& h_\theta(x) < 0.5 \rightarrow y = 0 \newline
\end{align*}
$
</div>

![decision boundary](/assets/posts/MachineLearning/ml3-3.png)

logistic function에서 z가 0보다 크면 g(z)는 항상 0.5보다 크다. 그리고 z가 0보다 작으면 항상 g(z)는 0.5보다 작다. 자연로그의 특성을 이용해서 logistic function의 성질을 정리하면 

<div>
$
\begin{align*}
z=0,  e^{0}=1,  g(z)=1/2\newline 
z \to \infty, e^{-\infty} \to 0, g(z)=1 \newline
 z \to -\infty, e^{\infty}\to \infty, g(z)=0 
\end{align*}
$
</div>

가 된다. logistic function의 입력 \\( z\\)는 \\( \theta^Tx\\)이므로

<div>
$
\begin{align*}
& h_\theta(x) = g(\theta^T x) \geq 0.5 \newline
& when \; \theta^T x \geq 0
\end{align*}
$
</div>

따라서

<div>
$
\begin{align*}
& \theta^T x \geq 0 \rightarrow y = 1 \newline
& \theta^T x < 0 \rightarrow y = 0 \newline
\end{align*}
$
</div>

가 된다. 수식이 많아서 복잡해 보이지만 마지막 결론만 알고 있으면 될 것 같다.



---

## Reference

  - [Causer Machine Learning class by Andrew Ng](https://www.coursera.org/learn/machine-learning/home/week/3)
  

---