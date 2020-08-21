# Git 기초

> Git은 분산형 버전관리시스템(DVCS)이다.

Git을 윈도우에서 활용하기 위해서는 [git bash](https://gitforwindows.org/)를 설치해야한다.



## 1. 저장소 초기화

```bash
$ git init
Initialized empty Git repository in C:/Users/i/Desktop/TIL/.git/

(master) $
```



* 로컬 저장소를 만들고 나면, `.git/` 폴더가 생성되고, bash에 `(master)`라고 표기된다.
* 반드시 저장소를 만들기 전에 원하는 디렉토리인지 확인하는 습관을 가지고, 저장소 내부에 저장소를 만들지는 말자.
  * 예) Desktop -> git 저장소, TIL -> 다른 git 저장소(x)



## 2. add

작업한 내용을 커밋 대상 목록에 추가한다.

```bash
$ git add .					# 현재 디렉토리(하위 디렉토리 포함)
$ git add a.html			# 특정 파일
$ git add b.html c.html		# 특정 다수 파일
$ git add blog/ 			# 특정 폴더
```





```bash
# 작업 후 상태
$ git status
On branch master

No commits yet
# Untracked files => Git으로 관리된적 없는 파일
Untracked files:
# 커밋될 것들에 포함시키기 위해서는 add 명령어를 써라
  (use "git add <file>..." to include in what will be committed)
        Setting.png
        git.md
        markdown-images/
        markdown.md
        "\353\204\244\353\252\250\353\260\224\354\247\200 \354\212\244\355\217\260\354\247\200\353\260\245.png"

# 총평
# 커밋될 곳에 없다(nothing)
# 하지만, 새로 생성한 파일(untracked files)은 존재한다.
nothing added to commit but untracked files present (use "git add" to track)

```

```bash
$ git add .
```

```bash
# add 명령어 후 상태
$ git status
On branch master

No commits yet
# 커밋이 될 변경 사항들
# working directory X
# Staging area O
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   Setting.png
        new file:   git.md
        new file:   markdown-images/Setting.png
        new file:   markdown.md
        new file:   "\353\204\244\353\252\250\353\260\224\354\247\200 \354\212\244\355\217\260\354\247\200\353\260\245.png"

```
[Local Area]
Working directory - add -> Staging Area - commit -> Version(commit)



## 3. commit

```bash
$ git commit -m 'Add markdown.md'
[master (root-commit) 17fe0c8] Add markdown.md
 5 files changed, 119 insertions(+)
 create mode 100644 Setting.png
 create mode 100644 git.md
 create mode 100644 markdown-images/Setting.png
 create mode 100644 markdown.md
 create mode 100644 "\353\204\244\353\252\250\353\260\224\354\247\200 \354\212\244\355\217\260\354\247\200\353\260\245.png"
```

* 커밋은 버전(이력)을 기록하는 명령어이다.
* 커밋 메시지는 해당하는 이력을 나타낼 수 있도록 작성하여야 한다.
* 커밋 이력을 확인하기 위해서는 아래의 명령어를 사용한다.

```bash
$ git log
commit 17fe0c89cdf66b84996398a47e3f916007f46255 (HEAD -> master)
Author: chochonghee <gontry2@naver.com>
Date:   Thu Aug 20 14:58:09 2020 +0900

    Add markdown.md

$ git log -1
$ git log --oneline
$ git log --oneline -1
```

```bash
$ git status
On branch master
nothing to commit, working tree clean
# working directory X, working directory X
```



## push to origin master

```bash
$ git remote add origin https://github.com/gontry2/TIL.git
$ git push -u origin master

Enumerating objects: 14, done.
Counting objects: 100% (14/14), done.
Delta compression using up to 8 threads
Compressing objects: 100% (11/11), done.
Writing objects: 100% (14/14), 33.50 KiB | 8.37 MiB/s, done.
Total 14 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), done.
To https://github.com/gontry2/TIL.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```



! denied 뜨면
자격증명 관리자에서 windows자격 증명에서 github.com 제거 후 다시 git push origin master

