---
layout: post
title: layout, _includes 그리고 포스팅
category: [DEV]
tag: [jekyll]
thread: [jekyll-tutorial]
description: jekyll의 _layout과 _includes를 알아보고 posting을 해보자.
---

지난 포스팅에서 jekyll을 설치하고 로컬환경에서 jekyll을 빌드해보았습니다. 이번 포스팅에서는 jekyll의 유명테마인 [hyde](https://github.com/poole/hyde)를 살펴보며 jekyll이 어떻게 구성되어있는지 살펴봅니다.

---

# 파일 구조
[hyde 테마](https://github.com/poole/hyde)를 받습니다. 해당 레포지토리를 fork한 후에 clone을 해도 좋고 **clone or download** 버튼을 눌러 다운로드하거나 git clone명령어를 통해 원하는 위치에 해당 저장소를 클론해도 됩니다. 가장 편하고 자신있는 방법으로 하이드 테마를 다운합니다.

다운로드/클론이 완료되었다면 코드편집기로 폴더를 열어줍니다.

```
├── 404.html
├── README.md
├── _config.yml
├── _includes
│   ├── head.html
│   └── sidebar.html
├── _layouts
│   ├── default.html
│   ├── page.html
│   └── post.html
├── _posts
│   ├── 2012-02-06-whats-jekyll.md
│   ├── 2012-02-07-example-content.md
│   └── 2013-12-28-introducing-hyde.md
├── about.md
├── atom.xml
├── index.html
└── public
    ├── apple-touch-icon-144-precomposed.png
    ├── css
    │   ├── hyde.css
    │   ├── poole.css
    │   └── syntax.css
    └── favicon.ico
```

코드편집기로 코드를 열면 위와같은 폴더/파일들이 보일겁니다. 그리고 hyde theme을 `jekyll serve`혹은 `jekyll s`명령어로 로컬환경에서 빌드를합니다. 그리고 접속을 합니다.

---

# index.html
**http://127.0.0.1:4000/** 혹은 **http://localhost:4000/** 에접속하면 가장 먼저 보이는 페이지가 바로 **index.html** 입니다.

해당파일의 가장 윗부분을 보면 html문법이 아닌 다른 요상한 문법으로 적힌 부분이 보입니다. 이부분은 [yaml](https://ko.wikipedia.org/wiki/YAML)로 작성된 부분인데 해당 페이지, 포스트가 어떤 정보를 가지고 있는지 명시되어있습니다.

```yaml
---
layout: default
title: Home
---
```

**index.html** 은 default layout에 렌더링되고 title이 home임을 알 수 있습니다. 그 다음 영역을 살펴볼까요

{% highlight html linenos %}
<div class="posts">
  {{ " {% for post in paginator.posts " }} %}
  <div class="post">
    <h1 class="post-title">
      <a href="{{ "{{ post.url" }} }}">
        {{ "{{post.title "}} }}
      </a>
    </h1>

    <span class="post-date">{{ "{{ post.date | date_to_string " }} }}</span>

    {{ "{{ post.content " }} }}
  </div>
  {{ " {% endfor " }} %}
</div>
{% endhighlight %}

마찬가지로 html문법이 아닌 녀석들이 보입니다. {{ "{{ "}}}} 혹은   **{{ " {%  " }} %}** 엮인 친구들은 [liquid](https://shopify.github.io/liquid/)라는 템플릿 언어입니다. 나중에 살펴볼 **_config.yml** 에 선언한 변수들 혹은 jekyll이 정적사이트를 만들면서 생성한 객체(pages, posts 등)를 렌더링할 때 사용됩니다. 위 코드는 현재 페이지에 속해있는 포스트듸 제목(6 행), 날짜(10 행), 포스트 내용(12 행)을 렌더링 하고 있습니다. 만약 **index.html** 에서 포스트의 제목만 노출하고 싶다면 12행을 삭제하면 됩니다.


{% highlight html linenos %}
<div class="pagination">
  {{"{% if paginator.next_page"}} %}
    <a class="pagination-item older" href="{{"{{ site.baseurl"}} }}page{{"{{paginator.next_page"}}}}">Older</a>
  {{"{% else"}} %}
    <span class="pagination-item older">Older</span>
  {{"{% endif"}} %}
  {{"{% if paginator.previous_page"}} %}
    {{"{% if paginator.page == 2"}} %}
      <a class="pagination-item newer" href="{{"{{ site.baseurl"}} }}">Newer</a>
    {{"{% else"}} %}
      <a class="pagination-item newer" href="{{"{{ site.baseurl"}} }}page{{"{{paginator.previous_page"}}}}">Newer</a>
    {{"{% endif"}} %}
  {{"{% else"}} %}
    <span class="pagination-item newer">Newer</span>
  {{"{% endif"}} %}
</div>
{% endhighlight %}
위 코드는 pagination이 렌더링 되는 부분인것 같네요 **Newer** 나 **Older** 같은 레이블이 맘에 들지 않는다면 해당 부분을 수정하면 되겠네요

# \_layouts/default.html
앞서 살펴본 **inedx.html** 에서 yaml에 layout을 선언하였습니다. layout은 포스트나 페이지를 포장할 때 사용하는 템플릿입니다. default.html의 코드를 살펴보도록 하겠습니다.

{% highlight html linenos %}
<!DOCTYPE html>
<html lang="en-us">

  {{"{% include head.html"}} %}

  <body>

    {{"{% include sidebar.html"}} %}

    <div class="content container">
      {{"{{ content"}} }}
    </div>

  </body>
</html>
{% endhighlight %}

11행에 default를 layout으로 선언한 페이지나 컨텐츠의 내용이 11행에 들어갑니다.

# \_inclues/sidebar.html
\_layouts/default.html의 4행과 8행을 보면 **include** 가 보입니다. include는 재사용을 위해서 파일을 담는 공간으로 포스트나 페이지 그리고 레이아웃에 쉽게 삽입할 수 있습니다. \_layouts/default.html코드에서 4번째 행에 미리작성된 \_includes/sidebar.html 를 가져와 해당 부분에 코드를 주입합니다. 반복되는 코드가 있거나 너무 길어져 따로 관리가 필요한 파일들은 **\_includes** 에 저장해서 따로 관리하면 편리하겠네요!

# \_posts
작성한 포스트가 저장되는 폴더입니다. 새 포스트를 작성하려면 해당 폴더에 파일을 생성하기만 하면됩니다. 이때 주의할 점은 파일 이름 형식에 맞게 파일이름을 지정해줘야합니다.
```
YYYY-MM-DD-title.md
```
위와 같이 4자리, 2자리, 2자리 숫자로 YEAR, MONTH, DATE를 쓰고 나머지 부분에 제목을 작성하면 됩니다. 지금 보고 계신 포스트의 제목은 다음과 같습니다.

```
2017-12-17-jekyll2-blog-a-post.md
```

이제 **\_post** 에 포함되어있는 파일을 하나 열어봅시다. 이전에 살펴본 **index.html** 과 같이 yaml머리말이 작성되어있습니다. 새로 포스트를 작성할 때 **layout** 과 **title** 그리고 **description** 을 작성해주면 됩니다.

# \_config.yml
사이트의 환경설정을 작성할 수 있는 파일입니다. 사이트의 이름, baseurl등을 지정할 수 있고 여러가지 옵션들을 추가 할 수 있습니다.

---

다음 포스트에서는 page를 작성하고 포스트의 tag과 category를 추가하는 방법을 알아봅니다.


## reference
- [jekyll 한글 문서](http://jekyllrb-ko.github.io/)
- [liquid](https://shopify.github.io/liquid/)
- [mastering markdown](https://guides.github.com/features/mastering-markdown/)
