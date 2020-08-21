# Git 원격 저장소 활용

Git 원격 저장소 기능을 제공해주는 서비스는 `gitlab`, `bitbucket`, `github` 등이 있다.



## 0. 원격 저장소 설정

```bash
$ git remote add origin {url}
$ git remote add origin https://github.com/gontry2/TIL.git
```

* git, 원격저장소를 추가(`add`)하고 `origin`이라는 이름으로 `url`으로 설정

* 설정된 저장소를 확인하기 위해서는 아래의 명령어를 사용한다.

```bash
$ git remote -v
origin  https://github.com/gontry2/TIL.git (fetch)
origin  https://github.com/gontry2/TIL.git (push)
```



## 1. 원격 저장소 복제

```bash
$ git clone {url}
```

* 해당 명령어를 입력한 위치에 원격저장소 이름으로 폴더가 생기며, 저장소가 복제된다.



## 2. 원격 저장소에 `push`

```bash
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

* 원격저장소(`origin`)의 `master` 브랜치로 기록된 커밋(버전)이 업데이트된다.



## 3. `pull`

```bash
$ git pull origin master
```

* 원격저장소(`origin`)의 `master` 브랜치에 기록된 커밋(버전)이 현재 로컬 저장소로 받아온다. (`fetch` + `merge`)