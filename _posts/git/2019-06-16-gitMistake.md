---
title: "git 실수 했을때 되돌리는 방법"
categories:
  - git
tags:
  - git
---
git을 쓰다가 실수로 파일을 올리거나, 올리거나, 올리거나 하는 실수를 해버려서
되돌리는 방법을 기록한다.

git add 취소
---
    $ git reset HEAD [파일명]
    
파일명이 없는 경우 add 한 전체 파일을 add 안한 상태로 돌려준다.


git commit 취소
---
    $ git reset HEAD^
    
commit 메시지 수정
---
    $ git commit --amend -m [수정할 메시지]
    
가장 최근에 commit 한 메시지 수정만 가능하다.

git push 취소
---
push 취소랄까 정확히 말하자면 잘못 올라간 파일 삭제하기!!  
이걸 위해 이 포스팅을 쓴거라 할 수 있다.

파일 삭제하기

    $ git rm [파일명]      // 로컬 저장소와 원격 저장소에 있는 파일 삭제
    $ git rm --cached [파일명]     // 원격 저장소에 있는 파일만 삭제하기
     
git rm 만 하는 경우에는 로컬과 원격에서 파일이 삭제된다.

요전에 내가 한 실수는 KEY 값이 있는 파일을 실수로 올린것이기 때문에, 로컬에는 파일이 있어야 하고, 원격에는 없어야 한다.
이때는 --cached 옵션을 넣어서 원격 저장소에 있는 파일만 삭제한다.
    
    $ git commit -m '파일삭제'
    $ git push
    
파일 삭제한 내역을 반영하기 위해 commit 하고 push  
근데 commit history 를 보면 삭제한 파일이 뭐였는지 확인 할 수 있음-_-
파일 내역 다 지우고 싶은데??????
    
    $ git filter-branch --force --index-filter \ 'git rm --cached --ignore-unmatch [삭제할파일명]' \--prune-empty --tag-name-filter cat -- --all
    
위 명령어로 삭제할 파일이 있는 history 내역을 삭제한다.

    $ echo "[앞으로 commit 안할 파일명]" >> .gitignore
    $ git add .gitignore
    $ git commit -m "Add YOUR-FILE-WITH-SENSITIVE-DATA to .gitignore"
    
실수로 중요 데이터가 더이상 commit 되지 않도록 .gitignore 파일에 해당 파일 이름을 추가하고 push 한다.

    $ git push origin --force --all
    
push 실행

제대로 잘 삭제 됐는지 확인하는건 필수!

참고링크 https://help.github.com/en/articles/removing-sensitive-data-from-a-repository