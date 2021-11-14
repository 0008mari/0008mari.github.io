---
layout: post
title: "지옥에서 온 Git"
date: 2021-11-11
categories: study
tags: [git, study]
---



이 문서는 공개 강좌 [지옥에서 온 깃](https://youtu.be/hFJZwOfme6w)을 보고 작성한 수업 노트입니다. 내용은 완벽하지 않으며 개인적으로 볼 의도로 작성하였습니다.



# 지옥에서 온 Git

# 수업소개

### 버전 관리 시스템

* 효용 - 백업 복원 협업
* 여러가지 버전 관리 시스템 존재. CVS, SVN, GIT
  * 버전 컨트롤 시스템의 본질적 요소 - 변경 사항을 관리한다
  * 혁신적인 요소 - 기존에 유행하던 CVS을 어떻게 SVN이 뛰어넘었는가? 시스템 간 차이점
* 버전 컨트롤 시스템은 복잡하고 어렵다.
  * 혁신에 혁신을 거듭하며 기능이 많이 추가되고 점점 어려워 짐.
  * Dropbox, Google Drive 등을 통해 우선 버전 컨트롤 시스템의 기초 (백업, 관리, 공유)를 볼 수 있음. 더 쉽고 간단한 시스템. 
* 그럼에도 GIT을 사용하는 이유 - 현실은 GIT보다 어렵다 
  * 프로젝트가 커질 수록 버전 관리가 필요하다.

# 버전 관리의 본질

## init, add, commit

### init

`init` 현재 디렉토리에서 새롭게 작업 시작

```bash
Initialized empty Git repository in C:/Users/00_ma/Documents/gitfth/.git/
```

`ls -al` 하면 현재 위치 아래에 `.git`이 생성되어 있음.

### add

간단한 파일 생성 후 버전 관리를 해보자. 실제로 git을 사용할 때에는 복잡한 여러개의 파일을 관리하게 되지만, 공부용이니까.

```bash
vim f1.txt
```

vim 사용법은 학교 유닉스 서버 쓰느라 강제로 배워짐 

```bash
cat f1.txt
```

파일 내용 미리보기 (굳이 vim으로 안 들어가고 배쉬 화면에서 확인 가능.)

```bash
git status
```

> On branch master
>
> No commits yet
>
> Untracked files:
>   (use "git add <file>..." to include in what will be committed)
>         f1.txt
>
> nothing added to commit but untracked files present (use "git add" to track)

아직 track 시작하지 않음. 

```bash
git add f1.txt
```

새로 추가한 파일은 git에게 버전 관리를 시작하도록 알려주어야 함. 임시 파일 등은 버전 관리를 할 필요가 없기 때문. 

### commit - 버전 만들기

버전은 의미있는 변화를 남겨두는 것이다.

git을 처음 사용할 때 이름을 세팅해야한다.

```bash
git config --global user.name 닉네임
git config --global user.email 이메일
```

이제 버전 정보에 이름과 이메일이 포함된다.

```bash
git commit
```

에디터가 실행된다. 기본 vim인데 나는 git 설치 시 vscode를 선택해서 vscode 창이 뜬다. 

커밋 메시지를 적고 닫으면 커밋 완료.

```bash
git log
```

> $ git log
> commit 5efca76e5dd92712526bf0a5cadd0b46b08bbaa3 (HEAD -> master)
> Author: 0008mari <0008mari@gmail.com>
> Date:   Thu Nov 4 22:19:47 2021 +0900
>
>     1 first commit message

수정을 해보자. `vim f1.txt`로 안의 내용을 고치고 

```bash
git status
```

> On branch master
> Changes not staged for commit:
>   (use "git add <file>..." to update what will be committed)
>   (use "git restore <file>..." to discard changes in working directory)
>         modified:   f1.txt
>
> no changes added to commit (use "git add" and/or "git commit -a")

빨간 색으로 **modified**라고 뜬다.

```bash
git add f1.txt
```

파일의 버전 관리를 시작할 때, 이미 버전 관리 중인 파일의 수정 후 버전 생성 시에 모두 `add`를 사용한다.

커밋 후 status를 하면 첫번째와 두번째 메시지가 나온다.

## stage area

왜 git은 `add`라는 과정을 포함하고 있는가? 그냥 커밋하면 되는데...

프로젝트가 크면 커밋 시기를 놓치게 된다. 원래 커밋은 하나의 작업만 담고 있는 게 인상적. 그러나 몰아서 커밋하다 보면 여러개를 한꺼번에 할 수도.

이 때 git에서는 add를 통해, 커밋하고자 하는 파일만 커밋시킬 수 있다.

### 실습

`f1.txt`, `f2.txt` 2개의 파일을 수정한다 (수정 내용 상관x)

스테이터스를 보면

> On branch master
> Changes not staged for commit:
>   (use "git add <file>..." to update what will be committed)
>   (use "git restore <file>..." to discard changes in working directory)
>         modified:   f1.txt
>         modified:   f2.txt
>
> no changes added to commit (use "git add" and/or "git commit -a")

이렇게 나오죠...

하지만 add f1.txt를 하고 스테이터스를 다시 보면

> On branch master
> Changes to be committed:
>   (use "git restore --staged <file>..." to unstage)
>         modified:   f1.txt
>
> Changes not staged for commit:
>   (use "git add <file>..." to update what will be committed)
>   (use "git restore <file>..." to discard changes in working directory)
>         modified:   f2.txt

이렇게 나옵니다. 똑같이 modified 인데 f1만 add 했기 때문에 f1만 커밋이 될 예정입니다.

`commit`을 하면 메시지를 쓰고 f1만 커밋이 됩니다.

다시 status를 해 보면 f2는 modified로 남아있는 것을 알 수 있다.

### 설명

* add의 기능 - 파일을 커밋 대기 상태로 만든다.
* git commit - 커밋 대기 상태의 파일만을 포함하여 버전 생성. 

이 때 커밋 대기 상태를 stage area라고 한다.

* stage: 커밋 대기를 하고 있는 파일들의 장소
* repository: 커밋 된 결과가 저장되는 장소. (저장소)

## 변경 사항 확인하기 log & diff

```bash
git log -p
```

`-p`: 버전 별로 소스의 차이점을 자세히 보여준다.

* +의 내용은 해당 커밋으로 변한 내용을 보여준다.
* -의 내용은 해당 커밋으로 변경된 내용을 보여준다.

### `-p` 옵션 살펴보기

> commit 154289f38abb09a9c9541eb2ef83a162f0c3816e (HEAD -> master)
> Author: 0008mari <0008mari@gmail.com>
> Date:   Thu Nov 4 22:50:08 2021 +0900
>
>     4th commit
>
> diff --git a/f1.txt b/f1.txt
> index 2456b16..9462317 100644
> --- a/f1.txt
> +++ b/f1.txt
> @@ -1 +1 @@
> -source : 2
> +f1.txt : 2

* `+f1.txt : 2`
  * 버전 4에서 f1.txt의 내용은 이것
* -source : 2
  * 버전 3에서는 이것이었다.

> commit 222b5726e4035c6da34cd3188090842876a6b048
> Author: 0008mari <0008mari@gmail.com>
> Date:   Thu Nov 4 22:40:18 2021 +0900
>
>     f2.txt is added
>
> diff --git a/f2.txt b/f2.txt
> new file mode 100644
> index 0000000..79a79f1
> --- /dev/null
> +++ b/f2.txt
> @@ -0,0 +1 @@
> +222222222

### 커밋 아이디

위의 버전을 보면 commit 뒤에 길게 나온 아이디가 있다.

커밋 아이디는 해당 버전의 고유한 주소이다.

예를 들어서 `222b5726e4035c6da34cd3188090842876a6b048` 이렇게 생겼다.

```bash
git log (아이디)
```

이렇게 하면 해당 버전 이전의 로그를 볼 수 있다.

### git diff

특정한 두 버전 간의 차이점을 id를 통해 알아볼 수 있다.

```bash
git diff (아이디1)..(아이디2)
```

중간에 점이 `..` 이렇게 들어가 있다.

```bash
git diff
```

방금 수정한 파일의 이름. 수정 내용. 지금 어떠한 작업을 했는지 알려준다!

커밋 전 자기가 작업한 내용에 문제가 있는지, 마지막 리뷰를 하는 기회!

만약 수정 후 `add`를 하고 `diff`를 하면, 아무것도 나오지 않는다.

### 요약

* 버전 별 차이점 `git log -p`

## reset - 과거로 돌아가기

git의 효용 중, 과거로 돌아가는 방법에 대해 알아보자.

커밋을 취소하는 명령. 조금 복잡하니 주의! 이렇게 한다 정도만 알아보고, git의 원리를 보고 다시 살펴보면 덜 혼란스럽고 덜 위험할 것이다.

* 안전하게 reset 하기?
  * `.git`을 포함한 폴더를 통째로 복사해두면 살릴 수 있다.

### reset 실습

5번째 버전을 3번째로 바꾸고 싶어요. 5와 4에 해당하는 커밋은 삭제할 거예요. 3번째 커밋을 최신 상태로 하고 싶어요. 

최신 상태로 하고 싶은 해당 커밋 아이디 카피.

```bash
git reset (아이디) --hard
```

`--hard`는 쉽고 위험한 방법. 추후 안전한 다른 옵션도 알아본다.

이후 git log를 하면 4와 5가 사라지고, 3이 가장 최신 상태임을 알 수 있다. 파일의 내용을 열어서 확인해봐도 3번째의 상태로 돌아가 있다.

### 설명

깃에서는 웬만하면 정보를 삭제하지 않는다. 지금 삭제된 것 처럼 보여도 어딘가에 정보가 남아 있음. 되돌리는 방법은 git의 이론을 보고 다시 살펴본다.

원격 저장소를 이용해 다른 사람과 협업하는 경우, reset을 사용하지 않는다.

### revert

이런 게 있는데, 현재 상태로는 다루지 않겠음. 

현재 상태로는 버전을 생성, 차이를 확인하는 방법을 아는 게 좋다. 리셋 굳이 x

## 스스로 공부하는 법

* 가장 자주 쓰이는, 중요도 높은 기초를 다진다.
* 모르는 것은 스스로 찾아봐서 알아낸다.

깃 공부에 적용하자면 이렇게 된다.

1. 가장 중요도 높은 것? 이미 거의 배웠다! commit add log diff 등.ㅇ
2. 어떻게 알아볼 수 있을까>
   * 예시: commit 시 한줄에 커밋 메시지까지 써서 날리고 싶다. 굳이 에디터 열 필요 없자나.
   * `git commit --help`
     * 매뉴얼이 나옵니다~
   * `git commit -m <msg>`
   * 매뉴얼을 보는 것이 쉽지는 않지만, 매뉴얼에 익숙해질 필요가 있다.

## 수련해봅시다

지금까지 배운 내용은 어떠한 버전 관리 시스템이든 가지고 있는 본질적인 부분이다. 이 이후로는 git이라는 제품이 가지고 있는 고유의 혁신적인 점을 살펴본다.

혼자서 프로젝트를 하는 상황이라면, 사실 지금까지 배운 것으로 충분할 수 있다. (난... 아닌듯) git의 세련된 백업에 대한 부분은 아직 배우지 않았지만, 드랍박스나 구글 드라이브에 `.git`이 포함된 폴더를 올리면서 백업하는 것으로 대체 가능하다.

git을 많이 써서 익숙해지자.

# git의 원리

## git의 원리 소개

* 원리를 왜 공부하는가?
  * 궁금하니까.
  * 원리를 알면 공부하기가 쉽다.
  * git의 원리에서 많은 영감을 얻을 수 있다.

가봅시다

## 분석도구 gistory 소개

git의 내부를 분석하기 위해, gistory를 이용해 보자.

명령에 따라 `.git`이 어떻게 변하는가? ㅎㅎ 직접 만드신 프로그램

수정된 파일들을 따라가며 살펴본다.

## git add

파일이 달라도, 내용이 같으면 같은 아이디로 취급된다. 중복 제거.

## object 파일명의 원리

objects/파일명

오브젝트를 객체라 한다.

파일명과 약간의 정보를 가지고 SHA1이라는 해싱을 거친 결과를 id 로 사용한다.

## commit의 원리

commit을 하면 그 버전이 마치 파일의 내용처럼 objects 내용으로 들어간다. 커밋도 객체다.

* tree: 커밋이 실행된 시점에, 디렉토리에 있던 파일들의 이름. 그리고 내용에 대한 링크 (id). 커밋마다 트리값이 다르다. 
  * snapshot. 각 버전은 각 버전이 만들어진 시점의 정보를 가지고 있다.

* parent: 해당 커밋에 대해 이전 커밋을 나타냄.

오브젝트 파일의 종류 3가지

* blob: 파일의 내용
* tree: 어떤 디렉토리의 파일명과 내용에 해당하는 blob 정보
* commit: 각 커밋에도 object id를 가지고 있다.

## status의 원리

인덱스는 무엇인가. 스테이터스의 원리는?

* git status에서 커밋할 것이 뭐가 있는지 없는지 어떻게 아는 걸까?
  * index의 내용과 가장 최신 커밋의 tree의 내용(해시  id)을 비교해, 차이점이 없다면 커밋할 것이 없는 것이다. (현재 디렉토리의 내용 = index 파일의 내용.)
  * modified 여부 역시 해시 아이디를 보고 알 수 있음.
* 3가지 단계의 저장소
  * workspace (working space) - 프로젝트 폴더라고 했던 것 .git 포함
  * index: 위에서 add한 파일들이 등록되는 곳 / staging area (커밋 대기 장소라는 의미에서) / cache
  * repository: 커밋한 파일들

# git의 혁신 - branch

## branch 소개

branch라는 것은 나무의 가지에 빗댄 개념.

예: 파일을 순차적으로 수정하며 숫자를 붙였다고 해보자. 그런데 이 파일이 순차적으로 변경되는 것이 아니고 가지를 치면서 복잡하게 -_- );;

* branch 생성: 작업이 분기되는 상황
* branch: 분기들 

기존의 버전 관리 시스템에도 branch 가 있었으나 무겁기 때문에 많이 사용되지 않았다. git에서는 이것을 잘 쓸 수 있게 만들었다.

## branch 만들기

### 실습

```bash
git commit -am "2"
```

옵션

* `-a`: 자동 add. 생성 이후 한 번이라도 add 했던 파일에 대해서만 작동. 
* `m "message"`: 커밋 메시지

```bash
git branch (브랜치명)
```

브랜치명 쓰면 새 브랜치 생성. 안 쓰면 현재 브랜치를 보여줌.

`* master`: 현재 사용 중인 기본 브랜치.

```bash
git checkout (브랜치명)
```

브랜치로 들어가기

생성된 브랜치는 속해있던 브랜치의 상태를 그대로 갖게 된다.

exp 브랜치에서 f1.txt의 내용을 수정하고 커밋해도, master 브랜치에는 변화가 생기지 않는다.

상당히 편리한 기능이지만, 복잡성이 따른다.

## branch 정보확인

```bash
git log --branches --decorate
```

해당 브랜치의 가장 최신 커밋에 레이블 붙어 있음.

HEAD: 현재 체크아웃된 브랜치가 적혀 있음.

`--graph`

각 브랜치가 다른 내용으로 가고 있는 경우, 그래프 옵션을 붙이면 보기가 편하다

`--graph` `--oneline`

위 그래프 모양을 더 요약해서 보여줌

```bash
git log A..B
```

A 브랜치에는 없고, B 브랜치에는 있는 커밋을 비교해서 보여준다.

`-p` 어떤 차이가 있는지까지 보여준다.

```bash
git diff A..B
```

A에 대해 B가 다른 점을 보여준다.

## branch 병합

 exp의 내용을 master로 옮기고 싶어. exp에서 작업했던 (master와 다른 ) 내용을 master도 갖게 하는 것이 목표.

```bash
git merge exp
```

master로 체크아웃 후 git merge exp

이제 exp 역시 master와 같은 내용으로 만들어보자. exp로 체크아웃.

```bash
git merge master
```

exp를 삭제한다. 다시 master로 체크아웃 후
```bash
git branch -d exp
```

## branch 수련

[Git Document: 브랜치와 Merge](https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%99%80-Merge-%EC%9D%98-%EA%B8%B0%EC%B4%88)

키워드만 적어둠

* fast-forward 병합
* recursive strategy

## stash

stash: 감추다, 숨겨두다.

한 브랜치에서 할 일이 다 끝나지 않았는데, 다른 브랜치로 체크아웃해서 작업해야하는 경우. 작업이 끝나지 않은 것을 커밋하기 애매함. 커밋을 안 하면 체크아웃 할 수가 없음. stash를 이용하면 커밋 없이 그 내용을 브랜치에 숨겨둘 수 있다.

커밋 안 하고 체크아웃 하는 경우 git status 했을 때 다른 브랜치에서 modified 된 내용까지 표시가 된다. 

```bash
git stash [save]
```

감춰두면 파일을 열었을 때 변경 사항이 나타나지 않음.

```bash
git stash apply
```

다시 불러오기

stash list해서 나오는 stash 내용은 명시적으로 삭제하지 않으면 남아 있다. 예를 들어서 이걸 커밋 안 하고 그 전 커밋으로 reset 한다고 해도 stash는 남아 있음. 삭제하는 법 `git stash drop`가장 최신의 스탯시를 삭제함

untracked file (add 되지 않은 파일) 은 stash가 적용되지 않는다.



# 원격 저장소

## 원격 저장소 소개

협업을 위해 필요하다

## 원격 저장소 생성

한 대의 컴퓨터 안에서 다른 저장소에 원격 저장소를 만들고 백업하는 과정. 자주 사용하는 과정이 아니니 따라가며 보고 안 된다고 해서 너무 걱정x

```bash
git init --bare remote
```

`bare--` 작업이 불가능, 순수 저장소. 저장된 내용의 무결을 보장하기 위해서.

```bash
git push
```

현재 지역저장소의 checkout인 master 브랜치를 원격 저장소에 같은 이름으로 올린다.

## Github 소개

원격 저장소는 직접 서버를 구축도 가능하나, 구축과 유지 관리가 쉽지 않다. 깃허브는 오픈소스 프로그램의 아지트 역할을 하는 서비스이다.

* fork
  * 남의 레파지토리를 나의 레파지토리로 복제한다.

### 실습

git bash

로컬 저장소에 gitsrc 디렉토리를 만들어 복사해온다.

```bash
git clone (원격저장소의 주소) gitsrc
```



## 원격 저장소 만들기 (Github)

깃헙에서 리포지토리 만들기 

원격 저장소와 로컬 저장소의 연동

* 원격 저장소를 만들고 그것을 복제해 로컬 저장소에서 작업
* 이미 로컬 저장소에서 작업하던 것을 원격 저장소로 업로드 

후자부터 보자

```bash
git remote add origin (깃헙주소)
```

origin 이라는 이름으로 원격 저장소 생성. 관습적으로 기본적인 원격 저장소를 origin 이라고 이름붙인다.

```bash
git remote -v
```

등록된 원격 저장소의 목록을 보여준다.

* push: 로컬 저장소 기준. 로컬 저장소에서 원격 저장소로 데이터를 push한다.

아까 본 첫번째 방법

```bash
git clone (주소) .
```

`.` 은 현재 저장소라는 의미다.

원격 저장소가 지역 저장소로 동기화 되어 있다.








# 번외 - bash 사용하기

윈도우우즈 유저의 경우 bash에서 여러 단축키가 먹히지 않아서 어버버 할 때가 있다.

## 복사, 붙여넣기

* 복사: `ctrl + shift + c`
* 붙여넣기: `shift + insert`

딴소리 - 로지텍 K380 블루투스 키보드를 사용하고 있는데, insert가 자주 사용하지 않아서 그런지 fn을 조합해야 누를 수 있다. 

## LF, CRLF

> warning: LF will be replaced by CRLF in f2.txt.
> The file will have its original line endings in your working directory

* CRLF - 윈도우에서 사용하는 줄바꿈 방법
  * `\r`, `\n`
* LF - Unix, Mac OS에서 사용하는 줄바꿈 방법
  * `\n` only

알아서 변환을 해준다고 하니 오케이라고 하면 됨. 

직접 하고 싶다면, **VScode**의 하단 바 참고. 인코딩 옆에 선택할 수 있도록 나와 있다.

## 윈도우에서 ls 쓰기

```
doskey ls = dir
```

