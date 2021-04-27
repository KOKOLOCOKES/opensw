# Git

리누스 토르발즈가 2주만에 자기가 쓰려고 만든 **분산 버전 관리 시스템**

> 힙한 리누스 토르발즈
>
> > `Git`은 그냥 아무 의미 없는 세글자 알파벳이라고 한다. 그냥 유닉스 명령어 중에 `git`이라는 명령어가 없어서 정했다고 한다. 기분이 좋으면 “global information tracker”라고 하고 기분이 구리면 “goddamn idiotic truckload of sh*t”이라고 하랜다.







## Git 용어

### Remote

리모트 서버 자체

이 서버를 제공해주는 대표적 업체.

Git을 만든게 아니라 Git이라는 시스템에 필요한 리모트 서버와 Git을 좀 더 편하게 사용할 수 있는 기능들을 제공하는 것.

=> `Github`, `Bitbuket`, `GitLab`



### Origin

Git을 사용할 때 내가 어떤 리모트 서버에 변경 사항을 업로드 할 것인지 정해야하는데,

반드시 하나의 리모트 서버만 사용할수 있는 것이 아니기 때문에 이름을 정해줘야한다.

근데 사람들이 자주 사용하는 관례적인 이름이 `Origin`



보통은 한 개의 리모트 서버만 운용하는 경우가 대다수이기 때문에 많은 사람들이 `Remote`와 `Origin`을 혼용해서 부르곤 한다.



### Repository

레파지토리(Repository, Repo)는 저장소라는 뜻

리모트 서버 내에서 구분되는 프로젝트 단위

일반적으로 한 개의 레파지토리는 하나의 프로젝트를 의미하지만 경우에 따라서 레파지토리 하나에 여러 개의 프로젝트를 구성하기도 한다.

Repo를 클론 받을 때에는 해당 레포를 가리키는 URL이 필요한데, 레포의 이름은 URL 가장 마지막에 `.git`이라는 확장자가 붙는다.



### Branch

독립된 작업을 진행하기 위한 작업공간의 개념

Git 을 초기화 했을때 기본적으로 `master`라는 매인 브랜치가 생성된다.

개발하는 기능 등에 따라 브랜치를 추가로 생성하고 작업한 후에 `master` 로 `Merge` 하는 과정을 거친다.

정리:

```
1. Git을 초기화하면 기본적으로 master 브랜치가 생긴다. 이 친구가 메인 브랜치 역할을 한다.
2. 브랜치는 어떤 브랜치에서 분리시키는 것이고, 분리된 브랜치는 분리될 당시의 부모 브랜치 상태를 그대로 가지고 있다.
3. 개발자는 각각의 브랜치에서 개발을 진행한 뒤 나중에 다시 master 브랜치로 변경 사항을 합친다.
```

`  git branch -vv`

브랜치 목록과 상태 확인



### Merge Conflict

내 작업물과 다른 사람의 작업물이 충돌한 상황

1. 꼭 push하기전에 pull을 해주면 conflict를 줄일 수 있다.
2. 여러명이 작업 할 때, 복잡한 작업을 할 때는 branch를 판다.

3. pull은 자주 해주기

<hr/>

## Git 필수 명령어



### clone

리모트 서버의 Repo에서 클라이언트로 파일을 복붙하는 행위

어떤 Repo에서 파일을 가져올것인지의 정보는 URL로 표현.

HTTPS방식과 SSH방식이 있다.

원하는 작업 디렉토리로 이동한 후 클론 받으면 된다.

```bash
cd ~
git clone https://github.com/repodajdla/afjl.git
```

클론 받으면 현재 위치에 레포 이름과 동일한 디렉토리가 생성되고 해당 리모트 서버의 레포의 소스가 전부 복사된다.



### pull

리모트 서버의 최신 소스를 가져와서 로컬 소스에 Merge하는 명령어

**Pull Request** 해줘~==내가 작업한 브랜치를 가져가서 합쳐줘~

```bash
$ git pull # 현재 내 로컬 브랜치와 같은 이름을 가진 리모트 서버 브랜치가 타겟
$ git pull origin master # origin 리모트 서버의 master 브랜치가 타겟
```





### fetch

리모트 서버의 최신 소스를 내 클라이언트로 가져오되 병합은 안하겠다.

`git fetch`

`fetch` 명령어를 사용하면 다른 사람들이 리모트 서버에 새로 업데이트한 모든 내역을 받아올 수 있다.





### add

내 클라이언트에서 어떤 소스를 보낼지 추가하는 것

어떤 물건을 보낼지 고른다 라고생각하면 됨

```bash
$ git add . # 현재 디렉토리의 모든 변경사항을 스테이지에 올린다
$ git add ./src/components # components 디렉토리의 모든 변경사항을 스테이지에 올린다
$ git add ./src/components/Test.vue # 특정 파일의 변경사항만 스테이지에 올린다
$ git add -p # 변경된 사항을 하나하나 살펴보면서 스테이지에 올린다
```

이때 선택된 변경 사항들은 `스테이지(Stage)`라고 불리는 공간으로 이동하게 된다.

이때 `git add <경로>` 명령어는 해당 경로 안에 있는 변경 사항을 전부 스테이지에 올리게 되는데,

이게 영 불안하다 싶은 사람은 `-p` 옵션을 줌으로써 변경 사항을 하나하나 확인하면서 스테이지에 올릴 수도 있다.



이렇게 스테이지에 담긴 변경 사항들은 `git status` 명령어를 사용하여 확인해볼 수 있고,

`status` 명령어에 추가적으로 `-v` 옵션을 사용하면 어떤 파일의 어떤 부분이 변경되었는지도 함께 볼 수 있다.

```bash
$ git add ./soruce
$ git status

On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   source/_drafts/git-tutorial.md
```



### commit

`add`한 것들을 하나의 버전으로 정의하는 과정

고른 물품을 포장한다고 생각하면 된다.

```bash
$ git commit -m "First commit"
```

커밋 기록 확인:

```bash
$ git log --graph

* commit 20f1ea9 (HEAD -> master, origin/master, origin/HEAD)
| Author: Evan Moon <bboydart91@gmail.com>
|
|     회원가입 기능 개발 끝!
|
* commit ca693fd
| Author: Evan Moon <bboydart91@gmail.com>
|
|     회원가입 비밀번호 입력 폼 추가
|
* commit f9b6e2d
| Author: Evan Moon <bboydart91@gmail.com>
|
|     회원가입 이메일 입력 폼 추가
|
```

각각의 commit 들은 20f1ea9 이런 해시값을 갖는다.

`git checkout ca693fd` 명령어로 회원가입 비밀번호 입력 폼이 추가된 시점으로 이동할 수 있다는 것이다. 즉, 시간여행이 가능하다!





### push



```bash
$ git push origin master # origin 리모트 서버의 master 브랜치로 푸쉬해줘!
```



Git 브랜치 자동 추적

```bash
$ git push --set-upstream origin master	
```

`--set-upstream` 옵션을 사용하고 처음 한번만 브랜치 이름을 입력해주면 그 이후로는 `git push` 명령어만 입력해도 자동으로 처음 입력했던 브랜치로 변경 사항을 푸쉬할 수 있다.



**clone -> 파일 수정 -> add -> commit -> push**