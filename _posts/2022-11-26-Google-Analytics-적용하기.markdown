---
title:  "Google Analytics 적용하기"
date:   2022-11-26
categories: [Blog Setting]
---


깃 블로그에 Google Analytics를 적용한 과정을 포스트로 작성해보자.  
[해당](https://infiduk.github.io/2019/11/05/google-analytics.html) [블로그](https://colliecollie.netlify.app/blog-jekyll-googleanalytics/)들의 포스트를 참고하여 적용했다.<br>

## 1. 계정 만들기
[구글 아날리틱스 홈페이지](https://analytics.google.com/analytics/web/)로 들어가 주어진 절차에 따라 계정을 생성했다.  
계정 이름, 데이터에 대한 권한, 데이터를 측정할 플랫폼과 웹 사이트를 설정해주었다.

<br>
## 2. 지킬에 적용하기
계정을 생성하고 웹 사이트를 등록하면 측정 ID가 생성된다. `관리` → `속성` → `데이터 스트림`에서 등록한 웹 사이트의 정보를 클릭한다.  
`스트림 세부정보` 메뉴에 측정 ID가 표시된다.
하단의 `Google 태그` 메뉴의 `태그 안내 보기`를 클릭하면	태그 설치 메뉴가 나타나는데, 이곳에서 직접 설치에 필요한 Google 태그도 찾을 수 있다.
```html
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-XXXXXXXXXX');
</script>
```
G-XXXXXXXXXX 자리에는 측정 ID가 들어가 있을 것이다.  
<br>
필자가 적용한 테마는 `_config.yml`파일에 추적 ID만 기입하면 자동으로 적용되도록 준비되어 있었다.  
그래서 일단 해당 기능을 적용해 보고, 성공적으로 적용되는 것을 확인한 후 관련 코드를 수정해서 직접 적용해 보았다.  
지킬의 `_include` 폴더 내의 `head.liquid` 파일의 코드에 관련 코드가 있는 것을 확인하고, 전부 주석 처리를 한 뒤 위의 Google 태그를 입력해 주었다.  
그 다음 모든 포스트에 해당 기능이 적용되도록`_layouts` 폴더 내의 `default.html` 파일 코드 헤드에 `{​% include default/head.liquid %​}`가 있는 것을 확인했다.  
깃허브에 푸쉬한 후 사이트에 접속한 결과 통계가 잘 적용되는 것을 확인했다.
