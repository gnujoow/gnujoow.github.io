---
layout: post
title: atom에서 linter를 사용해보자
category: [Dev]
description: atom에서 eslint를 이용하여 깔끔하게 코딩해보자.
tag: [atom, coding, eslint, linter, es6, javascript]
---

이 글을 읽기 전에 읽어보면 좋은 글  

- [**subicura** linter를 이용한 코딩스타일과 에러 체크하기](http://subicura.com/2016/07/11/coding-convention.html)

코딩을 하다보면 좀더 깔끔한 코드, 코딩스타일이 일관되게 유지되는 코드를 작성하고 싶은 욕심이 생기게됩니다. 짱짱한 회사들의 코딩스타일 문서[[1]](https://github.com/google/styleguide)[[2]](https://github.com/airbnb/javascript)를 살펴보며 평소 나의 코딩 습관과 비교해보고 나름의 노력도 해보지만 남이 보기에도 깔끔하고 일관된 코드를 작성하기란 쉽지 않습니다 ㅠㅠ.

특히 프로젝트를 진행할 때 각자 다른 코딩스타일을 가진 사람들이 코드를 작성하다보면 코드를 리뷰하거나 유지/보수할 때 어려움이 생기게 되는데, 나름의 규칙도 만들고 규칙을 문서화해서 노력해보지만 <del>특히 내 경우에</del> 평소의 습관이 종종 튀어나와 일관성을 해칠 때가 많았습니다.

**udemy** 에서 [**reactjs** 수업](https://www.udemy.com/react-redux/learn/v4/content)을 보면서 공부하고 있는데 최근에 강의 하시는 [Stephen Grider](https://github.com/StephenGrider)님이 **ESlint** 에 대해 다룬 [동영상](https://www.youtube.com/playlist?list=PL9f8_QifuTL4CS8-OyA-4WADhkddOnRS4)을 공개했습니다. 이번 포스팅에서는 이 동영상을 바탕으로 atom 코드 편집기에서 eslint를 설치하고 현재 진행하고 있는 [ReactJS 프로젝드](https://github.com/gnujoow/shim)의 코드를 깔끔하게 작성하는 과정에 대해서 정리해보도록 하겠습니다.

sublime text, vs code, webstorm을 사용하시는 분들은 **reference** 에 있는 링크를 확인하시면 됩니다.

---

> # linter  
**명사** 솜부스러기 채취기 [*네이버사전*](http://endic.naver.com/enkrEntry.nhn?sLn=kr&entryId=de2f89f5fdbc42e88f2ebf24e4ff0cf2)

![예1](/images/dev/4/0.png)

*출처 [ESlint overview](https://www.youtube.com/watch?v=aWFwJVjfDlE&index=1&list=PL9f8_QifuTL4CS8-OyA-4WADhkddOnRS4)*

Atom은 편집기의 기능을 확장할 수 있도록 여러 패키지들을 제공하고 있다. 우리는 Linter라는 패키지를 설치하면 atom 코드 편집기에서 Linter가 작동하게 된다.

세상에는 정말 많은 프로그래밍 언어가 있고 언어마다 선호하는 규칙이 전부 다르다. Linter 패키지는 각각 언어들의 규칙을 담고 있는 Linter를 포함하여 코드 편집기에서 검사를 할 수 있게 만든다. 지금 reactjs로 프로젝트를 진행하고 있으므로 ESlint라는 linter를 설치한다. ESLint 혹은 다른 언어의 linter는 코드 편집기에 작성된 코드들을 읽어서 규칙에 맞는지 검사하고 코드 편집기에 에러 메시지를 띄운다.

여기까지가 코드 편집기에서 설정하는 내용이다. 여기 까지 진행하고 코드편집기를 실행하면 아무런 메시지를 띄우지 않는다. 그 이유는 config 즉, ESlint이 되어있지 않기 때문인다. ESlint는 작성된 코드를 읽어서 config 에 정의된 규칙들을 적용하여 규칙에 맞지 않는 경우 에러 메시지를 띄우게된다. 프로젝트마다 추구하는 코딩 스타일이 다를텐데 적절하게 config를 설정하면 된다.

규칙들을 하나하나 추가하여 설정을 만들어도 되지만 인터넷에 공개되어있는 짱짱한 회사의 규칙이나 유명한 프로젝트의 규칙을 그대로 가져와서 사용하는 방법도 있다.

---

# 설치하기
![예1](/images/dev/4/1.png)
atom의 설정에서 install을 클릭하여 [linter-eslint](https://atom.io/packages/linter-eslint)와 [linter](https://atom.io/packages/linter)패키지를 설치한다. 여기까지가 코드 편집기에서 설정의 전부이다. 이제 ESlint가 적절한 규칙들을 불러올 수 있도록 설정해야한다.

airbnb에서 [javascript 스타일 가이드](https://github.com/airbnb/javascript)가 오픈소스로 공개되어있다. 이 규칙을 사용하기 위해 프로젝트의 루트 폴더에서 다음 명령어를 입력한다.


{% highlight shell %}
$ npm install --save-dev eslint-config-airbnb babel-eslint eslint-plugin-react
{% endhighlight %}

![예1](/images/dev/4/2.png)
atom에 설치한 ESlint패키지가 설정파일을 불러올 수 있도록 `.eslintrc` 파일을 프로젝트의 루트폴더에 만들어준다.

![예1](/images/dev/4/3.png)
**.eslintrc** 파일에 우리가 사용할 규칙을 명시해주면 설정 끝

이제 편집하던 모든 소스파일들을 종료하고 다시 켜보자. 그럼 linter가 규칙에 맞지않게 작성된 코드들을 보여준다.
![예1](/images/dev/4/4.png)

에러 메시지를 [클릭](http://eslint.org/docs/rules/class-methods-use-this)하면 어떤 규칙을 지키지 않았는지 그리고 규칙에 대한 코딩스타일을 볼 수 있다. 이를 보고 다시 수정하면된다.

# 규칙수정하기
![예1](/images/dev/4/5.png)
linter와 문서를 보며 정리한 코드 확실히 에러 메시지가 줄었고 코드도 훨씬 깔끔해졌다. 그런데 이 부분의 에러는 문서를 읽어봐도 잘 모르겠고 왜 나는 에러인지 잘 모르는 부분이 있었다.

![예1](/images/dev/4/6.png)
이렇게 규칙이 빡빡하다고 생각하거나 조정이 필요한 경우 규칙을 수정할 수 있다.

아까 추가한 `.eslintrc`파일에서
{% highlight json %}
{
  "extends": "airbnb",
  "rules": {
      "class-methods-use-this": 0
    }
}
{% endhighlight %}

[class-methods-use-this](http://eslint.org/docs/rules/class-methods-use-this) 항목을 0으로 설정하고 다시 코드 에디터에서 에러난 부분을 확인하면

![예1](/images/dev/4/7.png)
새로운 규칙이 적용되어 에러메시지가 뜨지 않는것을 확인할 수 있다.

지금 현재 적용하여 사용하고 있는 규칙은 아래와 같습니다.

{% highlight json %}
{
  "extends": "airbnb",
  "rules": {
      "class-methods-use-this": 0,
      "comma-dangle": 0,
      "react/prop-types": 0
    }
}
{% endhighlight %}

---

# 마치며
난생 처음으로 linter를 설치하고 규칙을 적용하여 코딩을 해보았습니다.  
linter를 설치하고 규칙을 설정하고 그리고 규칙에 맞게 코딩하는 과정이 고되긴 하지만 코딩스타일이 훨씬 깔끔해진것 같고 유지보수하기 편해진 코드가 된것같아 자신감이 조금 상승한것 같네요 :)
<del>코딩 잘 하고 싶다.</del>

---

## reference
- [**Rally Coding** ESLint Overview and Setup](https://www.youtube.com/playlist?list=PL9f8_QifuTL4CS8-OyA-4WADhkddOnRS4)
- [**subicura** linter를 이용한 코딩스타일과 에러 체크하기](http://subicura.com/2016/07/11/coding-convention.html)
- [**_Jbee** Linter란 무엇인가?](http://asfirstalways.tistory.com/276)
- [**darokel** Setup ES6+Babel+JSX Linting with Atom](https://gist.github.com/darokel/90fe5c8ad8df5efcab6b)
- [**wikipedia** Coding conventions](https://en.wikipedia.org/wiki/Coding_conventions)
- [**wikipedia** Programming style](https://en.wikipedia.org/wiki/Programming_style)
- [**NHN** NHN 코딩 컨벤션](http://nuli.nhncorp.com/data/convention/NHN_Coding_Conventions_for_Markup_Languages-v2.75_open.pdf)
