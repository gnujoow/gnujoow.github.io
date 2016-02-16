---
layout: post
title: ML7::Advice for Applying Machine Learning
category: [Machine Learning]
tag: [Machine Learning,Diagnostic]
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

가설함수 평가하기

![예1](/assets/posts/MachineLearning/ml6-0.png)
