---
layout: post
title: jekyll을 설치해보자
category: [DEV]
tag: [jekyll]
thread: [jekyll-tutorial]
description: 정적 사이트 생성기인 jekyll을 설치해보자
---

[jekyll](https://jekyllrb-ko.github.io/)은 좋습니다. 그리고 jekyll + [github pages](https://pages.github.com/)은 정말 좋습니다.

github pages가 기본적으로 지원하는 정적 사이트 생성 라이브러리고, 개발자에게 친숙한 markdown 문법으로 문서를 작성하면 블로그 페이지가 뚝딱 만들어집니다. 따로 호스팅에 대한 고민할 필요 없고 도메인도 *username.github.io* 처럼 geek하고 개발력이 높아 보이는걸로 무료로 사용할 수 있습니다. 그리고 매일 블로그를 작성하다보면 매일 commit이 쌓이고 일년을 뒤돌아 봤을때 성장한 내 모습을 돌아보며 뿌듯함을 느낄 수 있구요.

![예1](/images/jekyll/lazy_year.png)
> 게을럿던 나의 지난 2017년...

git과 친숙하지 않은 개발자라면 블로그 포스트를 작성하면서 자연스럽게 commit, push와 같은 명령어와 가까워집니다. 그리고 욕심이 생기면 html, css를 수정해서 나만의 테마를 만들어서 배포할 수 있습니다 :)

---

jekyll은 **정적 웹사이트(static website)** 생성기입니다. 정적 웹 사이트는 서버에 미리 저장된 HTML, 이미지, javascript 파일등이 그대로 전달되는 웹페이지입니다. 사용자는 서버에 저장된 데이터가 변경되지 않는 한 고정된 웹페이지를 보게됩니다.

때문에 블로그, 간단한 소개페이지등 제한된 용도로만 사용할 수 있습니다만... 블로그로 사용하기에는 충분하다고 개인적으로 생각합니다.

---

정성사이트 생성기는 정말 많습니다. [staticgen](https://www.staticgen.com/)를 보면 많은 생성기가 있는데 jekyll이 star가 제일 많은 것을 확인 할 수 있습니다. 이 포스트에서는 star가 가장 많은! jeyll에 대해서 다루지만 다른 생성기들도 살펴보시고 만들고싶은 사이트 목적에 맞는 생성기를 선택하시면 좋을 것 같습니다.

---

# 설치하기

jekyll을 설치하기 위해서는 **ruby** 가 설치되어있어야 합니다.

다음 명령어를 통해 ruby가 설치되어있는지 확인할 수 있습니다.

```shell
$ ruby -v
```

ruby가 설치되어있지 않다면 [https://rvm.io/](https://rvm.io/)에 나온 설명을 따라 설치할 수 있습니다.


```shell
$ gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
```
```shell
$ \curl -sSL https://get.rvm.io | bash -s stable
```

첫번째 명령어에서 `command not found: gpg`과 같이 오류가 발생한다면 패키지 관리자인 **[brew](https://brew.sh/)** 를 통해 해당 패키지를 설치할 수 있습니다.

```shell
$ brew install gnupg gnupg2
```
> 참고 [stackoverflow](https://stackoverflow.com/questions/27041885/how-to-resolve-gpg-command-not-found-error-during-rvm-installation)

위 명령어들을 통해 **rvm**(Ruby Version Manager)가 설치되었습니다. 이제 ruby를 설치합니다.

```shell
$ rvm install 2.3.3
```

---

## jekyll 설치하기

ruby설치가 완료되었다면 이제 jekyll을 설치해야합니다. ruby에서는 라이브러리를 gem이라고 부르는데 다음 명령어를 통해서 jekyll을 설치할 수 있습니다.

```shell
$ gem install jekyll
```

jekyll 설치가 완료되었다면 다음 명령어를 입력해보겠습니다.


```shell
$ jekyll new my-new-blog
$ cd my-new-blog
$ jekyll s
```
위 명령어들을 통해 jekyll로 정적 웹페이지를 생성하였습니다.

---

다음 포스팅에서는 [hyde](https://github.com/poole/hyde)테마를 가지고 jekyll을 살펴보도록 하겠습니다.
