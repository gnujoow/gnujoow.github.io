---
layout: post
title: ReactJS에서 Mocha로 Test해보기
category: [ReactJS]
description: 난생 처음 ReactJS에 Test를 적용해본 경험기
tag: [ReactJS, ES6, Mocha, Chai, TDD, Test]
---

# 시작하기전 이야기
[동아리](http://likelion.org/)에서 만난 [친구](https://github.com/pjhjohn)와 함께 [jsonplaceholder-client](https://github.com/pjhjohn/jsonplaceholder-client)라는 프로젝트를 진행하고있다.

프로젝트는 [https://jsonplaceholder.typicode.com/](https://jsonplaceholder.typicode.com/) 이 사이트에서 제공되는 임의의 데이터를 받아 적절하게 reactJS로 <del>간지나게</del> 구현해보는 약간 sandBox느낌의 프로젝트인데 프로그래밍을 공부하면서 한 번도 test를 경험해본적이 없어 이번기회에 Test를 적용해보고 소프트웨어에서 테스트가 어떤 의미를 갖는지 생각해보기로 했다.

---

# 테스트 시작하기
테스트에는 [MochaJs](https://mochajs.org/), [chaiJS](http://chaijs.com/)를 사용하였다.  
다른 테스트 도구로는 [Jest](https://facebook.github.io/jest/), [enzyme](http://airbnb.io/enzyme/docs/future.html)등이 있다.

각각의 프레임워크와 라이브러리는 홈페이지에서 다음과 같이 소개하고 있다.

[MochaJs](https://mochajs.org/)
> **Mocha** is a feature-rich JavaScript test framework running on [Node.js](https://nodejs.org/ko/) and in the browser, making asynchronous testing simple and fun. **Mocha** tests run serially, allowing for flexible and accurate reporting, while mapping uncaught exceptions to the correct test cases.

[ChaiJS](http://chaijs.com/)
> **Chai** is a BDD / TDD assertion library for node and the browser that can be delightfully paired with any javascript testing framework.  
**Chai** has several interfaces that allow the developer to choose the most comfortable. The chain-capable BDD styles provide an expressive language & readable style, while the TDD assert style provides a more classical feel.

**Mocha** 는 Node.js 와 브라우저에서 작동하는 **JS 테스트 프레임워크** 로 테스트를 연속적으로 수행하며 테스트가 진행되는 동안 처리하지 않은 예외(uncaught exceptions)에 대해서 정확하고 유연하게 보고해준다는 특징이 있다. **Chai** 는 테스트 **라이브러리** 로 다른 JS 테스트 프레임워크와 함께 사용하기 좋고 TDD와 BDD 인터페이스를 제공한다.

## 설치

[프로젝트](https://github.com/pjhjohn/jsonplaceholder-client) 는 **npm** 으로 패키지를 관리하고 있으므로 npm으로 테스트 관련 패키지를 설치한다.

```
$ npm install --save-dev chai chai-jquery jquery jsdom mocha react-addons-test-utils
```

## `test_helper.js` 파일 작성하기
우리가 작성한 reactJS 컴포넌트들은 [webpack](https://webpack.github.io/)으로 빌드되어 `bundle.js` 하나의 파일로 만들어진다. 이 파일은 **brower** 에서 실행된다. 하지만 우리가 테스트를 실행하는 환경은 **terminal** 이므로 ㅌ테스트가 진행될 command line 환경인 terminal에서 마치 브라우저에서 실행되는것 처럼 환경을 만들어야한다.

이를 위해 [**jsdom**](https://github.com/tmpvar/jsdom)을 설치한다.
> A JavaScript implementation of the WHATWG DOM and HTML standards, for use with Node.js.  

[**jsdom**](https://github.com/tmpvar/jsdom)은 terminal에서 `bundle.js`가 실행되는것 처럼 시뮬레이팅(?)하는 도구이다.

프로젝트폴더에 `/test` 폴더를 만들고 여기에 `test_helper.js`를 만들고 아래 코드를 추가하자.

{% highlight js linenos %}
import jsdom from 'jsdom';
import jquert from 'jquery';

cosnt code = '<!document html><html><body></body></html>';
global.document = jsdom.jsdom(code);
global.window = global.document.defaultView;
const $ = jquery(global.window);
{% endhighlight %}

5행과 6행의 코드를 통해 전달받은 html문서(code)를 테스트 할 수 있는 환경을 만들 수있다.[참고](https://github.com/tmpvar/jsdom#for-the-hardcore-jsdomjsdom)

그리고 특정 `DOM`에 접근하기 위해서 jquery를 사용하는데 우리가 만든 global.window의 DOM에 접근할 수 있게 설정한다.

## 컴포넌트 렌더링
터미널이 브라우저처럼 작동하게 설정하는 단계는 마무리되었다. 이제 reactComponent를 테스트환경에서 렌더링해보자.
React 문서의 [Test항목](https://facebook.github.io/react/docs/test-utils.html#renderintodocument) 을 보면 html문서에 React컴포넌트를 렌더링하는 방법에 대해 명시되어 있다. `renderIntoDocument`함수를 사용하면 컴포넌트를 렌더링 할 수 있는데 이를 위해서는 `ReactDom`이 반드시 필요하다.


{% highlight js linenos %}
import ReactDom from 'react-dom';
import TestUtils from 'react-addons-test-utils';

<!--
이전 코드들
-->
function renderComponent(componentClass){
  const componentInstance = TestUtils.renderIntoDocument(<componentClass />)

  return $(ReactDom.findDOMNode(componentInstance));
}
{% endhighlight %}


---

코드의 양이 적거나

---

## reference

- [감성프로그래밍 - mocha로 javascript 테스팅 시작하기](http://programmingsummaries.tistory.com/383)
- [Alience Community - BDD와 TDD의 차이](http://blog.aliencube.org/ko/2014/04/02/differences-between-bdd-and-tdd/)
