1. 깃이란? -> 버전관리 도구

git 특징 및 장점

1) 빠른속도
2) 분산형 저장소 지원 (여러 명이 동시에 수정하는 환경에 적합)
3) 비선형적인 개발 (수천 개의 동시 다발적인 branch)
4) 완벽한 분산
5) 리눅스 커널 같은 대형 프로젝트에도 유용함 (속도나 데이터 크기 면에서)


2. GIT 실습

git 설치 후 가장 먼저 해주어야 할 설정
user.name
user.email
: 커밋시 author, committer 의 메타데이터로 사용

$ git config --global suer.name "YOUR NAME"
$ git config --global suer.name "YOUR EMAIL"

기존 프로젝트를 관리하고 싶을 때
$ git init 
새로운 디렉토리를 생성하여 git 저장소를 만들 때
$ git init (directory path)


3. 용어 정리

Git directory
.git 프로젝트의 프로젝트의 메타데이터와 객체 데이터베이스를 저장하는 곳

Working directory
프로젝트의 특정 버전을 checkout한 영역

Staging area (index)
저장할 파일들에 대한 정보를 담고있는 파일
	내가 저장하고 싶은 파일들만 올리는 것

Git 파일 관리 3단계
Woring directory 수정 -> staging area git add -> commit해서 영구적인 스냅샷을 올림

현재 working directory 상태 확인
$ git status

staging area로 올리기
$ git add /file path /file name
$ git add README.md

4. 파일 커밋하기

간단한 메시지를 남기며 커밋
$ git commit -m "simple message"
자세히 남기기
$ git commit 
(message 입력 후) esc -> wq -> enter

5. git diff
working directory 와 index를 비교
$ git diff

커밋 간 차이점을 비교
$ git diff (commitA) .. (commitB)

index와 HEAD를 비교
$ git diff --staged

5. git log
$ git log

6. git branch
branch 목록 확인
$ git branch 
branch 만들기
$ git branch
branch 삭제하기
$ git branch -d (branch_name)
-d는 merge된 branch만 삭제 -> 안전 장치가 있다?
-D는 그냥 생으로 branch 삭제
새로운 branch를 만들고 그 branch 로 변경
$ git checkout -b (branch_name)

실습
$ git branch fix/readme --> git branch 생성
$ git checkout fix/readme --> branch 이동
$ git checkout -b cfs

branch를 변경하면 일어나느 일들
- index와 working directory의 파일들이 변경된 branch를 기준으로 switching
- HEAD가 가리키는 branch가 변경됨

git merge
merge 하기
$ git merge (target_branch_name)

주의할 점 
코드가 반영될 branch에서 실행해야한다.

$git checkout fix/readme
$ vi README.md
$ git add README.md
$ git commit -m "fix README.md"
$ git checkout master
$ git merge fix/readme

fast-forward merge?
"현재 branch (수정된 코드가 반영될 branch)의 커밋이 변경이 일어난 branch(merge를 하려는 branch)의 base commit과 동일한 경우

fast-forward merge가 안 되는 경우 -> 3-way merge
- 두 branch간 공통의 parent commit을 이용하여 순차적으로 merge를 수행
- merge의 결과를 별도의 commit object로 저장
- 코드가 반영된 branch가 바라보는 commit을 새로 만들어진 commit으로 변경
- 이때 만들어진 commit을 merge commit이라고 함

3-way merge 실습 시나리오
- deview cfs 사이트를 만든다
- 이미 만들어 두었던 cfs branch에서 작업 후 master branch로 merge
- merge 된 cfs branch는 삭제
내가 작업을 했는데 아무도 추가를 하지 않으면 그대로 들어감
$ git checkout cfs
$ git add
$ git commit -m "add cfs hello.html"
$ git checkout master
$ git merge cfs
$ git branch -d cfs

branch 합치기 다른 방법
git rebase
- 지정한 base를 기준으로 현재 branch의 base commit을 변경
- 내부적으로는 base commit 을 기준으로 현재 branch 에서 추가된 변경을 하나씩 적용
- merge 와 log history자체가 변경 되기 때문에 호불호가 많이 갈리는 기능

git rebase는 한 줄로 commit을 관리할 수 있다.

git rebase시 주의점
- base commit을 기준으로 커밋을 새롭게 만들기 때문에 상당한 conflict 상황이 발생 가능
- 작업 history가 유지 되지 않게 되므로 작업 이력이 중요한 경우에는 적절하지 않음
- 개념을 잘 이해하지 못하고 사용하게 되면 더욱 큰 고통에 시달리게 됨

git remote 명령어
원격 저장소 추가
$ git remote add (remote alias) (remote url)
원격 저장소 상세정보 확인
$ git remote show (remote alias)
원격 저장소 alias 변경
$ git remote rename (old_name) (new_name)
원격 저장소 url 변경
$ git remote set-url (remote alias) (new remote url)
원격 저장소 목록 확인
$ git remote -v 

이미 존재하는 저장소 받아오기
git clone
- 이미 프로젝트가 진행되고 있어 remote repository가 존재하는 경우
- 새로운 개발장비에 개발 환경을 세팅 해야하는 겨웅
- 현재 작업중인 directory 외에 프로젝트를 복사 하고 싶은 경우 등등

remote 저장소를 local에 clone 하기
$ git clone (remote_url) [directory name] -b [branch name]
생략시 remote repository명으로 만들어 짐, 생략시 default branch로 받아옴

원격저장소 변경내용 가져오기
git fetch, git pull

fetch
remote 저장소에 추가된 object들을 받아와서 local에 저장
$ git fetch (remote) (remote branch)

pull
remote 저장소에 추가된 object들을 local로 받아오면서 merge까지 수행
fetch + merge
$ git pull origin master : 현재 작업중인 branch에 merge


