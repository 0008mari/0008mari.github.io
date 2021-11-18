---
layout: post
title: "블로그 꾸미기"
date: 2021-11-19
categories: blog
tags: [blog]
---

# 블로그 꾸미기

github 블로그에 jekyll 깔아서 사용 중, 테마는 minimal-mistake

한국어로 된 참고 자료도 있고 참 좋다.

블.꾸 과정임

## to do

* 본문 좌우여백 만들기 (지금은 너무 붙어 있다)
* 배경색, 글씨색 변경 
* 왼쪽 사이드바의 프로필 작성
* 패비콘 추가 (적당히 스마일)
* 카테고리 추가

## in progress

* 소제목에 있던 read-time을 포스트 업로드 날짜로 수정해준다. 방금 이걸 했는데 폰트 사이즈가 작아지고 제목에 걸려 있던 bold 표시도 사라졌다.
  * [커밋 변동사항](https://github.com/0008mari/0008mari.github.io/commit/a93a02579a543ac30f3d7c6b98ac85afa34f995d)
  * 참고중 https://devinlife.com/howto%20github%20pages/github-pages-settings/

## done

* 깃허브가 경고하는 보안 표시 없애기
  * path-parse를 1.0.7 이상으로 업데이트해야 한다고.
  * [변동사항](https://github.com/0008mari/0008mari.github.io/commit/b0d58e2ea9c76d421b3c08c97752ca776cc7b736)
  * 무지성으로 숫자만 바꿨는데 먹힌 것 같다.