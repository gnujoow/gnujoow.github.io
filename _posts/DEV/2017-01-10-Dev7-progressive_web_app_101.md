layout: post
title: 프로그레시브웹앱에 대해서 알아보자
category: [Dev]
description:
tag: [progressive webapp]
---

https://www.ampproject.org/ko/

프로그레시브 웹엡은 google의 개발자 Alex Russell이 2015년 6월 처음으로 제안한 아이디어라고 한다. [링크](https://arc.applause.com/2015/11/30/application-shell-architecture/)

프로그레시브 웹 앱은 다음과 같은 조건을 만족해야 한다.
- Reliable
  - Load instantly and never show the downasaur, even in uncertain network conditions.
  - 오프라인 상황에서도 빠르게 앱을 로드할 수 있어야한다.
- Fast
  - Respond quickly to user interactions with silky smooth animations and no janky scrolling.
- Engaging
  - Feel like a natural app on the device, with an immersive user experience.
  - 브라우저에서 바로 빠르고 간결한 동작으로 홈스크린에 앱을 설치할 수 있어야한다.
  - 그리고 브라우저가 닫혀 있어도 푸시를 제공할 수 잇어야한다.

구글은 이를 만족하는 웹 앱을 만들기 위해서 Application shell architecture와 service worker 두 가지를 내 놓았다.

**App shell** 은 progressive web app을 제공하기 위해 갖춰야하는 최소한으로 요구되는 HTML, css, JavaScript이다. 이들은 스피드에 포커싱된 구조로.
앱같이 보여주고 빠른 로딩을 돕는 녀석들이다. 말 그대로 앱의 껍데이기며 관련된 파일만 로컬에 캐싱해놓아 컨텐트가 로딩될 때만 그 안에 렌더링 해준다.



## reference
[로드쇼 슬라이드](https://github.com/pwa-workshop/roadshow)
[코드랩 자료](https://github.com/pwa-workshop/namp-card)
[Service Worker 101](https://goo.gl/6l28Zv)
[Service Worker 201](https://goo.gl/wWtBq0)
[서비스워커](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers?hl=ko)
