---
layout: post
title: "readme는 대문자? 소문자?"
date: 2021-12-21
categories: tips
tags: "tips"
---


# readme는 대문자? 소문자?

오늘의 궁금증은 자주 작성하게 되는 파일명인 `readme`가 대문자인지? 소문자인지? 입니다.

결론부터 말하면 관습적으로는 **대문자**입니다.

리눅스 파일 시스템에서는 대문자 이름이 가장 먼저 나오고,  `README.txt` 이렇게 작성하면 여러 파일 중 가장 위에 위치할 수 있습니다. 그리고 주목도가 높기 때문에 (영어에서 대문자는 강조의 의미도 있으니까) 더더욱! 이것을 보라는 의미가 있지 않을지... 

실제로 그런지 알아보기 위해 github를 켰습니다.

오픈소스 몇 개만 보자!

* cpython: `README.rst`
  
  * [cpython/README.rst at main · python/cpython · GitHub](https://github.com/python/cpython/blob/main/README.rst)

* Node.js: `README.md`
  
  * [node/README.md at master · nodejs/node · GitHub](https://github.com/nodejs/node/blob/master/README.md)

* Apache Hadoop: `README.txt`
  
  * [hadoop/README.txt at trunk · apache/hadoop · GitHub](https://github.com/apache/hadoop/blob/trunk/README.txt)

이것을 보아하니 관습적으로 **대문자**로 쓰는 것이 일반적인듯 합니다.



추가로, NOTICE, BUIDING, LICENSE, README 등 읽어야할 파일은 대문자로 쓰고, 그 외에 사람이 읽지 않는 파일 (소스)의 경우 소문자로 표기하는 것을 알 수 있었습니다.



궁금증 해결!
