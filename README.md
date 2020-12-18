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