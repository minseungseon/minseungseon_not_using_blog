---
layout: default
title: 02 git 
parent: Git
grand_parent: Git and Documents
nav_order: 2

---

오픈소스 PR, Review 과정 예시

- Contributing.md 꼭 읽어보기
    - 코딩 스타일 어떻게 할지, 등에 대해 나와 있음 
    - 코딩 바뀐거를 Before: After: 로 설명해줘도 좋음
    - 커밋을 나눠야 하는경우? 
        - 커밋 하나가 어떤 단위가 적절한걸까? 
        - 목적에 맞춰서 커밋을 나눌 수 있다. 
        - 리뷰, discussion 이 필요없으면 커밋은 길어도 된다.
        - 최초 커밋이면 시작지점이니까 길어도 괜찮은. 
    - 넣는대로 머지가 되는게 좋은건 아니다!


Issue/Disscusion 과정 예시
- Issue 는 첨부파일 이런 것 없이 글만 제시하는 것
- 자신이 어떤 버전을 쓰는데, 어떤 문제가 났다고 설명을 해야한다. 
- Label을 달 수 있다! critical, bug, question, document enhancement, 등이 있다.  
- 파일도 첨부할 수 있다 (퍄일 drag, drop 하면 바로 링크가 생김!)
- 91번 commit 있으면, 그 이슈를 해결하는 커밋이 있다면 그 안에서 Fixes #91이라고 메세지에 써서 커밋을 하면 표시가 된다!

커밋 메세지 작성하기
- file system의 ext4에서 B 문제를 해결했다 
    타이틀: fs ext4: fix B problem  
    내용: why:, how: 를 적을 수 있다. 

why:
how:

before:
after:

it is related with the commit 4e56led "fs ext4: Add B Feature"

fixes #91

reviewed-by: Namhyung Kim <~@gamil.com>

이러한 것들을 명시할 수 있다!

