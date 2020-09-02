# GIT Flow

>   Git을 활용하여 협업하는 흐름으로 branch를 활용하는 전략을 의미한다.

![git-flow_overall_graph](markdown-images/git-flow_overall_graph.png)


## 기본 명령어

* 브랜치 목록

```bash
$ git branch
```

* 브랜치 생성

```bash
$ git branch {브랜치이름}
```

* 브랜치 이동

```bash
$ git checkout {브랜치이름}
# 브랜치 생성 및 이동
$ git checkout -b {브랜치이름}
```

* 브랜치 병합

```bash
(master) $ git merge {브랜치이름}
```

{브랜치이름}을 (master)로 병합

* 브랜치 삭제

```bash
$ git branch -d {브랜치이름}
```



### 상황 1. fast-foward

> fast-foward는 feature 브랜치 생성된 이후 master 브랜치에 변경사항이 없는 상황

1. feature/blog branch 생성 및 이동

```bash
$ git checkout -b feature/blog
Switched to a new branch 'feature/blog'

(feature/blog) $
```

2. 작업 완료 후 commit

```bas
...
$ git add .
$ git commit -m 'Complete blog app'
```

3. master이동/ 병합

```bash
$ git checkout master
Switched to branch 'master'
$ git merge feature/blog
Updating c023ada..d6d004e
Fast-forward
Updating d6d004e..6c5fbda
Fast-forward
 blog.html | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 blog.html
```

4. 결과 -> fast-foward (단순히 HEAD를 이동)

```bash
$ git log --oneline
6c5fbda (HEAD -> master, feature/blog) Complete blog app
d6d004e hellobranch
c023ada Init, root commit이 반드시있어야함
```



5. branch 삭제

```bash
$ git branch -d feature/blog
Deleted branch feature/blog (was 6c5fbda).
```





### 상황 2. merge commit

> 서로 다른 이력(commit)을 병합(merge)하는 과정에서 다른 파일이 수정되어 있는 상황
>
> git이 auto merging을 진행하고, commit이 발생된다.

1. feature/poll branch 생성 및 이동

   ```bash
   (master)
   $ git checkout -b feature/poll
   Switched to a new branch 'feature/poll'
   ```

   

2. 작업 완료 후 commit

   ```bash
   $ touch poll.html
   $ git add poll.html
   $ git commit -m 'Complete poll app'
   [feature/poll ef2594f] Complete poll app
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 poll.html
   ```

   

3. master 이동

   ```bash
   $ git checkout master
   Switched to branch 'master'
   ```

   

4. master에 추가 commit 발생시키기

   ```bash
   $ touch hotfix.css
   $ git add .
   $ git commit -m 'hotfix in master'
   [master 5b553d1] hotfix in master
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 hotfix.css
   ```

   

5. master에 병합

   ```bash
   $ git merge feature/poll
   Merge made by the 'recursive' strategy.
    poll.html | 0
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 poll.html
   ```

   

6. 결과 -> 자동으로 merge commit 발생

   * vim 편집기 화면이 나타납니다.
   * 자동으로 작성된 커밋 메세지를 확인하고, `esc`를 누른 후, `:wq`를 입력하여 저장 및 종료를 합니다.
     * w: write
     * q: quit
   * 커밋을 확인해봅시다.

7. 그래프 확인하기

   ```bash
   $ git log --oneline --graph
   *   809c983 (HEAD -> master) Merge branch 'feature/poll' into master
   |\
   | * ef2594f (feature/poll) Complete poll app
   * | 5b553d1 hotfix in master
   |/
   * 6c5fbda Complete blog app
   * d6d004e hellobranch
   * c023ada Init, root commit이 반드시있어야함
   ```

   

8. branch 삭제

   ```bash
   $ git branch -d feature/poll
   Deleted branch feature/poll (was ef2594f).
   ```

   



### 상황 3. merge commit 충돌

> 서로 다른 이력(commit)을 병합(merge)하는 과정에서 동일 파일이 수정되어 있는 상황
>
> git이 auto merging을 하지 못하고, 해당 파일의 위치에 라벨링을 해준다.
>
> 원하는 형태의 코드로 직접 수정을 하고 merge commit을 발생시켜야한다.

1. feature/board branch 생성 및 이동

   ```bash
   $ git checkout -b feature/board
   Switched to a new branch 'feature/board'
   ```

   

2. 작업 완료 후 commit

   * readme 파일 수정 후 아래 명령어

     ```bash
     $ touch board.html
     $ git status
     On branch feature/board
     Changes not staged for commit:
       (use "git add <file>..." to update what will be committed)
       (use "git restore <file>..." to discard changes in working directory)
       # 추후에 마스터에서도 README를 고쳐서 충돌 발생시킬 예정
             modified:   README.md
     
     Untracked files:
       (use "git add <file>..." to include in what will be committed)
             board.html
     
     no changes added to commit (use "git add" and/or "git commit -a")
     $ git add  .
     $ git commit -m 'Complate board and update README'
     [feature/board afc7732] Complate board and update README
      2 files changed, 1 insertion(+)
      create mode 100644 board.html
     $ git log --oneline
     afc7732 (HEAD -> feature/board) Complate board and update README
     809c983 (master) Merge branch 'feature/poll' into master
     5b553d1 hotfix in master
     ef2594f Complete poll app
     6c5fbda Complete blog app
     d6d004e hellobranch
     c023ada Init, root commit이 반드시있어야함
     ```

3. master 이동

   ```bash
   $ git checkout master
   ```

4. master에 추가 commit 발생시키기!!

   * 동일 파일을 수정 혹은 생성하세요!

     ```bash
     # README 수정 후 commit
     $ git add README.md
     $ git commit -m 'Update README'
     [master c13e264] Update README
      1 file changed, 1 insertion(+)
     $ git log --oneline
     c13e264 (HEAD -> master) Update README
     809c983 Merge branch 'feature/poll' into master
     5b553d1 hotfix in master
     ef2594f Complete poll app
     6c5fbda Complete blog app
     d6d004e hellobranch
     c023ada Init, root commit이 반드시있어야함
     ```

     

5. master에 병합

   ```bash
   $ git merge feature/board
   Auto-merging README.md
   # 내용 충돌
   # README.md에서 충돌
   CONFLICT (content): Merge conflict in README.md
   # 자동 병합 실패
   # 충돌을 고치고, 다시 커밋해라!
   Automatic merge failed; fix conflicts and then commit the result.
   
   (master|MERGING) $ git status
   On branch master
   You have unmerged paths.
   # 충돌 고치고 commit!
     (fix conflicts and run "git commit")
     (use "git merge --abort" to abort the merge)
   # 커밋될 변경사항
   Changes to be committed:
           new file:   board.html
   # 병합되지 않은 파일들
   Unmerged paths:
   # 해결하고 add해!
     (use "git add <file>..." to mark resolution)
           both modified:   README.md
   ```

6. 결과 -> merge conflict 발생

7. 충돌 확인 및 해결

   ```bash
   <<<<<<< HEAD
   def index(request):
   	return 
   =======
   def create(request):
   	return 
   >>>>>>> feature/board
   ```

   ```bash
   # master에서 수정함
   ```

   * 수정 후에는 반드시 해당 파일 add

     ```bash
     $ git add .
     ```

8. merge commit 진행

   ```bash
   $ git commit
   ```

   

9. 그래프 확인하기

   ```bash
   $ git log --oneline --graph
   *   ac7bf81 (HEAD -> master) Merge branch 'feature/board' into master
   |\
   | * afc7732 (feature/board) Complate board and update README
   * | c13e264 Update README
   |/
   *   809c983 Merge branch 'feature/poll' into master
   |\
   | * ef2594f Complete poll app
   * | 5b553d1 hotfix in master
   |/
   * 6c5fbda Complete blog app
   * d6d004e hellobranch
   * c023ada Init, root commit이 반드시있어야함
   ```

   

10. branch 삭제

    ```bash
    $ git branch -d feature/board
    Deleted branch feature/board (was afc7732).
    ```

    

## Github Flow

### 1. shared repo (초대를 받은 경우)

* (merge를 local에서 안하고) branch에서 작업하고, 거기서 push
* pull request를 보냄 (reviewer 선택가능)
* merge하면 합쳐짐



### 2. Fork (초대를 받지 않은 경우)

* 다른사람의 repo를 Fork함
* 본인 github 저장소를 clone
* 내용 수정 후, commit
* 본인 github로 push
* pull request를 보냄