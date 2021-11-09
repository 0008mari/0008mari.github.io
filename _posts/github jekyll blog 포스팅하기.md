---
layout: post
title: "github jekyll blog 포스팅하기"
date: 2021-11-10
category: blog
tags: [jekyll blog]
---

# github jekyll blog 포스팅하기

도저히 방법이 외워지지 않아서 문서로 작성.

준비물: 마크다운 문서

## 1. convention

문서 최상단에 다음과 같은 정보를 기입한다.

```
---
layout: post
title: "제목"
date: 2021-11-10
category: hello
tags: [first, second]
---
```

* category는 따로 설정할 필요 없이 동적으로 작동한다. 한 가지만 가능.
* tag는 여러개 가능. 카테고리보다 좀 더 세부적으로
* 파일명은 `yyyy-mm-dd-title`

 이렇게 준비된 파일을 이미 세팅된 폴더 `_posts`안에 넣는다.

## 2. 원격 저장소에 push

git bash를 켜서 `_posts` 폴더까지 간다.

```bash
git add .
git commit -m "post commit message"
git push
```

원격 저장소에 올리기 전에 로컬호스트에서 미리 보고 싶은 경우에는 이렇게 한다.

```bash
bundle exec jekyll serve
```

## 3. 기타

불편하다... 마크다운 문서에 일일히 convention 언제 붙이고 앉아 있지? 이것도 찾아보면 자동화 할 수 있을 것 같다.