---
layout: post
title: 0.A la russe Algorithm
category: [algo]
tag: [Algorithm, multiplication, a la russe]
description: 곱셈 알고리즘 중 하나인 a la russe알고리즘에 대해서 알아보고 알고리즘의 C++ 표현을 알아보자.
---

사람이 곱셈을 할 때는 구구단을 이용해서 곱셈을 한다. **45 x 37**을 연산한다고 하면

= 45x(30+7)

= (45x30)+(45x7)

= 1350+315

= 1665

와 같이 연산을 한다. 하지만 곱셈의 복잡도는 더하기 보다 더 크기 때문에 컴퓨터에서 계산하게 되면 시간이 더 오래걸린다. 따라서 곱셈을 덧셈으로 바꿔서 풀면 표현은 더 길어지지만 좀 더 빠르게 풀 수 있다. 이를 사용해서 곱셈을 푸는 알고리즘을 **A la russe** algorithm 또는 **농부 곱셈법**이라고 한다.

[위키피디아](https://ko.wikipedia.org/wiki/%EA%B3%A0%EB%8C%80_%EC%9D%B4%EC%A7%91%ED%8A%B8_%EA%B3%B1%EC%85%88%EB%B2%95#.EB.86.8D.EB.B6.80_.EA.B3.B1.EC.85.88.EB.B2.95)


{% highlight cpp %}
#include <iostream>
using namespace std;

int main()
{
	int a, b;
	int result = 0;
	cin >> a >> b;
	
	while (a != 0)
	{
		if (a % 2 ==1)
			result += b;

		a = a >> 1;
		b = b << 1;

		cout << a << '\t' << b << '\t' << result << '\n';
	}

	cout <<"\n\n answer \t : \t"<< result << '\n';

	return 0;
}
{% endhighlight %}