---
layout: default
title: 01 git 
parent: Git
grand_parent: Git and Documents
nav_order: 1

---


## goorm 리눅스(컨테이너)  
컨테이너는 리눅스를 의미한다  
오리지널은 아니지만, 새로운 리눅스를 할당하게된다  
pytorch를 사용하게되는데, 셋팅의 시간을 줄여준다!  
conventional way로 pytorch를 로컬에 설치할 수 있긴 하다(github.com/pytorch/pytorch)  

이름 바꾸기
mv pytorch-example/ examples

또는 
git clone https://github.com/minseungseon/pytorch-example.git 원하는폴더이름

이렇게 해도된다! 

cat README.md


소스폴더 안에 example이 존재하기도 하고, python main.py 이런식으로 터미널에서 테스트도 해볼 수 있다.  


오픈소스에서 누가 제일 개발을 많이 한지 확인 할 수 있다
nl 명령: 파일의 line number 명시 ( 순위표시용 )
git shortlog -sn | nl
git shortlog -sn | nl | less

개발자별 commit 개수 요약 
git shortlog -h | grep summary 

개발자별 commit 개수 순위 정리
git shortlog -h | grep number 
-n, --numbered        sort output according to the number of commits per author

merge commit을 위해 만들어진 빈 커밋
-sn --no-merges | nl |less

전체 소스파일 수정내역(커밋) 개수 세기  
git log --oneline | wc -l

전체 소스파일 수정내역(커밋) ,라인 실행 후 q 눌러서 나갈 수 있음 
git log --oneline
git log --oneline --no-merges

commit ID: 소스파일 수정내역 고유한 ID (SHA1 해쉬값)  
특정 commit ID 의 내용 보기:
git show 0adb584376
git show commitID 

이렇게 하면, 커밋의 author, date, time, 내용(summary)까지 다 나온다  


해당 커밋에서 수정한 파일들 확인하기 
git show 0adb584376 | grep "diff --git"

해당 커밋에서 수정한 파일 개수 확인하기
git show 0adb584376 | grep "diff --git" | wc -l

merge한 커밋 확인하기
git show 머지커밋ID  

오픈소스 작업 폴더로 이동
cd /workspace/pytorch/examples

특정 폴더를 기준으로 소스 수정내역 리스트 확인하기
git log --oneline -- mnist/

특정 기간내 수정내역 리스트 확인
git log --oneline --after=2020-01-01 --before=2020-06-30
git log --oneline --after=2020-03-01 --before=2020-06-30 | wc -l //기간내 수정내역 커밋 개수

소스파일 수정내역 옛날것부터 살펴보기, 최초 커밋이 언제인지를 궁금할 때 가능하다 
git log --reverse

오픈소스 개발참여준비를 위한 git 설정
1. 오픈소스에 올릴 때, id/pw 캐싱 문제가 생길 수 있음
미리 읽어놓은 데이터인 캐싱데이터를 삭제하면 좋다(github id/pw 캐싱데이터를 삭제)
다른 깃헙 계정과의 충돌을 방지한다

git config --global --unset credential.helper
git config --system --unsert credential.helper

근데 다른 노트북을 쓰고있거나, 내 계정이 두개 이상이 아닌 이상 안해도됨


2. 차후 소스코드 파일수정 내역 저자 정보
저자정보가 없으면 누가 했는지를 알 수가 없다!

git config --global user.email "lisa71631999@naver.com"
git config --global user.name "MinseungSeon"

3. 편집기 설정하기(설명글 수정할 기본 편집기, vim, emacs, nano 등 모두 가능)
git config --global core.editor nano

sudo apt install -y nano

4. git 설정 내용 확인하기 
git config --list 

root@goorm:~/examples# git config --list
user.email=lisa71631999@naver.com
user.name=MinseungSeon
core.editor=nano
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
remote.origin.url=https://github.com/minseungseon/pytorch.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
branch.master.remote=origin
branch.master.merge=refs/heads/master

이렇게 추가가 된 것을 확인 할 수 있다


오픈소스 개발참여를 위한 수정 작업 
1. 브랜치 만들기
git checkout -b fix-mnist

**브랜치 이름은?
작업내용을 대표하는 키워드로 생성하는게 좋다!

2. 브랜치 삭제하기 
git checkout master
git branch -d fix-mnist

3. 원하는 편집기로 mnist/main.py 수정하기
nano mnist/main.py
저장: ctrl+o
나가기: ctrl+x

내가 수정한 내용 확인하기 
git diff

4. 커밋하기
git add mnist/main.py (특정 파일만 add)
git add . (모든 파일 add)
git commit -m " 내가 쓰는 메세지 "

5. commit 확인
git log --oneline -2 //2개만 보여주기 

잠시 저장하기 --> 커밋하기 애매하고, 날리기 애매할 때 저장할 수 있다. add 하고 commit 을 할 수는 있는데, 일단 임시저장을 한다. stash 로 저장한거는 pop으로 다시 복구 시킬 수 있다. 
작업을 하다가 애매모호하게 안끝났는데 테스트 해야할 때 많이 사용할 수 있다. 
임시저장:
git stash

임시저장한 것 복구하기:
git stash pop

git checkout -- mnist/main.py
이렇게 checkout 을 수정한 파일에 대해서 쓰게되면, 
mnist/main.py를 최신 history 로 부터 복구를 시키게 된다(기존의 것으로 모두 override 되고, 수정한 라인들은 모두 날라간다)

그러면, checkout 과 stash 의 차이는?
stash 는 저장
checkout은 복구

add 취소학
git reset

commit 정보 삭제하기(HEAD~1 은 가장 위에서 첫번째 내용을 삭제한다는 의미이다 )
git reset --hard HEAD~1 


라이센스를 잘 이해했다는 서명의 의미넣기

git commit -sm "Add import requests"

commit 4df855ce547453b183dfb51196442057f2a48327 (HEAD -> fix-mnist)
Author: MinseungSeon <lisa71631999@naver.com>
Date:   Sat Aug 1 10:32:48 2020 +0000

    Add import requests

    Signed-off-by: MinseungSeon <lisa71631999@naver.com>

이렇게 signed-off-by 한줄이 추가되어서 커밋이 된다. 

새로운 커밋을 만들지 않고 수정할 수 있다. 
git commit --amend 

이렇게 최신 commit 수정 이후 commit ID확인하기
git log --oneline -1


origin 은 fork를 뜬 것이다
upstream 은 rebase 를 위해 사용하는 것이다!

git remote add upstream 주소

//공식 upstream 저장소에서 최신 commit history 가져오기
git fetch upstream master

//최신 commit history 기준으로 베이스 갱신(rebase)
git rebase upstream/master

//Fork 한 저장소(Github)도 수정하기(PR 자동 갱신)
git push --force origin fix-mnist



되감기
git rebase -i --root 

**interactive 

열리는 파일에서 pick을 edit으로 수정한다!(원하는 시점에 edit을 하면 된다)

되감기를 취소하기(감았던 것을 푼다)
git rebase --continute 

예를들어서 예전으로 되감고, 세번 커밋을 한후 rebase --continue 를 하게 되면 중간에 세개의 커밋을 추가될 수도 있다. 

해당 소스파일을 누가 수정했고 언제 수정했는지 소스라인 기준으로 commit 정보를 찾아낼 수 있다.
git blame cmds/record.c


커밋 A,B,C 3개 합치기
git rebase -i --root 
해서 과거의 역사를 본다
B 커밋에 edit을 걸면, C 커밋이 없어진다. 

git reset --soft HEAD~1 (HEAD~1: 가장위에서 첫번째거 , --soft 파일내용은 안지우고 커밋만 지움)

git commit --ammend 


git rebase --abort : 했던 것 취소 


_____
B와 C를 먼저 합치고 A를 합쳐야지!
git rebase -i --root
에서 
C를 edit으로  바꾼다. 

과거로 돌아옴!
git reset --soft HEAD~1 
git commit --ammend 

이렇게 하면, 내용은 남고 커밋만 없어진 C와 HEAD가 된 B가 합쳐진다.  
최신 커밋(B)이 C와 흡수가 되는 것이다


