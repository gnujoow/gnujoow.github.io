---
layout: post
title: ML7::Advice for Applying Machine Learning
category: [Machine Learning]
tag: [Machine Learning,Diagnostic, Model Selection, Validation]
description: 머신러닝 알고리즘을 실제 문제에 적용할 때 고려할만한 요소에 대해서 알아보자.

---

머신러닝 알고리즘을 실제 문제에 적용할 때 고려할만한 요소에 대해서 알아보자.


## Deciding What to Try Next

linear regression을 처음 배웠을 때를 생각해보자. linear regression을 이용해서 집 값을 예측하는 문제를 풀었었는데 우리가 배운 regularization등 여러 기법들을 적용하여 가설함수(hypothesis function)를 얻었지만, 이를 적용 해본 결과 에러가 너무 큰 결과를 얻었다.ㅠㅠ

그럼 에러를 줄이고 더 좋은 가설 함수를 얻기위해서 아래 항목들을 시도해 볼 수 있다.

 - training example을 더 얻는다 / 더 많은 데이터를 알고리즘을 학습시키는데 사용한다.
 - 데이터의 더 적은 특징들을 사용해본다.
 - 데이터의 특징을 더 사용해본다.
 - polynomial 한 특징들을 사용해본다. \\((x^2 등등)\\)
 - \\(\lambda\\)를 크게 해본다.
 - \\(\lambda\\)를 작게 해본다.

위 항목들중에 아무거나 골라서 사용하는것이 아니라 Machine Learning Diagnostic를 통해서 적절한 조치를 취한다. 

## Evaluating a Hypothesis

가설함수 평가하는 방법과 underfit과 overfit을 방지하는 방법에 대해서도 알아보자.

우선 overfitting한 가설함수(hypothesis function)을 생각해보자. 이전 포스팅에서도 다루었듯이 overfitting된 가설함수에 새로운 데이터를 예측하면 잘 안되는걸 알 수 있다. 그럼 우리가 학습을 통해서 얻은 가설함수가 overfitting된다는 걸 어떻게 알 수 있을까?

linear regression에서 특징이 하나인 경우 대충 계산을 해서 우리가 직접 가설함수를 그릴 수 잇었다. 하지만 특징이 매우 많아질 경우 그려진 가설함수의 모양이 어떻게 될지 예측하기 힘들거나 불가능하다. 그렇다면 가설함수의 모양이 구불구불한 정도를 가지고 overfitting한 정도를 구분하기 힘들기 때문에 다른  방법으로 가설함수를 평가해야한다.

일반적으로는 다음방법으로 가설함수를 평가한다.

![예1](/assets/posts/MachineLearning/ml7-0.png)

여기 10개의 데이터셋이 있다고 하자. 이중에서 랜덤으로 7개를 뽑아 training set이라고 하고 나머지 3개를 test set이라고하자. 우선 학습알고리즘으로 training set을 통해 학습을 시켜서 가설함수를 만들고, 만들어진 가설함수에 test set의 데이터들로 테스트를 한다.

### Linear regresiion 에서 테스트

일반적으로 linear regression에서 테스트를 할 때에는 다음과 같은 절차를 따른다고 한다.

전체 데이터에서 랜덤하게 뽑은 70%의 데이터를 가지고 알고리즘을 학습시킨다.(비용함수의 값이 최소가 되도록)

그리고 **test set error**를 계산한다. test set error계산하는 데이터셋은 위에서 선택한 70%의 데이터를 제외한 30%의 데이터로 구한다.

<div>
$
J_{test}(\Theta) = \dfrac{1}{2m_{test}} \sum_{i=1}^{m_{test}}(h_\Theta(x^{(i)}_{test}) - y^{(i)}_{test})^2
$
</div>

### classification 에서 테스트

classification 문제에 사용되는 logistic regression 알고리즘의 테스트는 어떻게 할까?

linear regression과 비슷하게 전체 데이터중 랜덤하게 뽑은 70%의 데이터를 이용하여 알고리즘을 학습시키고 나머지 30%의 데이터로 **Misclassification error**를 구한다. Misclassification error는 말 그대로 얼마나 잘 못 구한것인지를 구하는것이다.

<div>
$
err(h_\Theta(x),y) =
\begin{matrix}
1 & \mbox{if } h_\Theta(x) \geq 0.5\ and\ y = 0\ or\ h_\Theta(x) < 0.5\ and\ y = 1\newline
0 & \mbox otherwise 
\end{matrix}
$
</div>

위와 같이 가설함수의 값이 0.5보다 큰데 0으로 분류되고, 가설함수의 값이  0.5 보다 작은데 1로 분류된 경우 1을 반환하고 잘 분류 된 경우에는 0을 반환한다.

그리고 이 에러에 대한 평균은 다음과 같이 구한다.


<div>
$
\text{Test Error} = \dfrac{1}{m_{test}} \sum^{m_{test}}_{i=1} err(h_\Theta(x^{(i)}_{test}), y^{(i)}_{test})
$
</div>


## Model Selection and Train/Validation/Test Sets

알고리즘을 선택하기 없어 가설함수를 몇차(**polynomial**)로 표현할 것인지, 어떤 **특징**들을 알고리즘을 학습시키는데 사용할 것인지 regularization을 할 때 \\(\lambda\\)값을 어떤걸 선택할지 결정해야 할 때 어떻게 해야할까? 이러한 문제는 **Model selection problem**라고 한다.
데이터를 train set과 test set으로 나누는 법과 train, validation, test sets으로 바꾸는 법도 알아보자. (맞는표현인지 모르겠다. 영알못...)

이전 포스팅에서도 많이 다뤘지만 가설함수(hypothesis function)이 training set에 대해서 너무 잘 표현된다면 overfitting이 일어난다는 것을 알고 있다. 이는 새롭게 추가되는 데이터에 대해서 가설함수가 제대로 적용도지 않기 때문이다.

그럼 본격적으로 model selection problem에 대해서 이야기해보자.