# 포크해놓은 저장소 동기화(?) 하기

1. 원본 저장소를 upstream 으로 추가한다 ([출처](https://help.github.com/articles/configuring-a-remote-for-a-fork/)):

    ```
	$ git remote -v
    origin https://github.com/자신의_아이디/자신의_포크.git (fetch)
    origin https://github.com/자신의_아이디/자신의_포크.git (push)
    ```

	...라고 나오면, 이 리포지토리 역시 추가해주어야 한다:

    ```
	$ git remote add upstream https://github.com/남의_아이디/원본_저장소.git
    ```

	이 리포지토리가 새로운 업스트림이 되었음을 확인한다:

    ```
	$ git remote -v
    origin https://github.com/자신의_아이디/자신의_포크.git (fetch)
    origin https://github.com/자신의_아이디/자신의_포크.git (fetch)
    upstream https://github.com/남의_아이디/원본_저장소.git (fetch)
    upstream https://github.com/남의_아이디/원본_저장소.git (push)
    ```

2. upstream 리포지토리에 올라온 브랜치와 각각의 커밋들을 `fetch` 로 받아온다. `master`에 올라온 커밋은 `upstream/master` 이라는 로컬 브랜치에 저장된다 ([출처](https://help.github.com/articles/syncing-a-fork/)):

	```
    $ git fetch upstream
    remote: Counting objects: 75, done.
    remote: Compressing objects: 100% (53/53), done.
    remote: Total 62 (delta 27), reused 44 (delta 9)
    Unpacking objects: 100% (62/62), done.
    From https://github.com/남의_아이디/원본_저장소.git
	 * [new branch]      master     -> upstream/master
    ```

3. 자신의 포크에서 `master` 브랜치를 체크아웃한다:

    ```
    $ git checkout master
    Switched to branch 'master'
    ```

4. `upstream/master` 에서의 변경사항을 자신의 로컬 `master` 브랜치로 병합한다. 이렇게 함으로서 업스트림 리포지토리의 내용을 자신의 포크의 `master` 브랜치와 (작업 내용을 잃지 않고) 동기화한다.

	```
    $ git merge upstream/master
    Updating a422352..5fdff0f
	Fast-forward
	 README                    |    9 -------
	 README.md                 |    7 ++++++
	 2 files changed, 7 insertions(+), 9 deletions(-)
	 delete mode 100644 README
	 create mode 100644 README.md
    ```

    만약 자신의 로컬 리포지토리에 변동사항이 없었다면, "fast-forward" 가 실행된다:

    ```
    $ git merge upstream/master
    Updating 34e91da..16c56ad
	Fast-forward
	 README.md                 |    5 +++--
	 1 file changed, 3 insertions(+), 2 deletions(-)
    ```
