---
title: " reset 과 revert"
categories:
  - git
tags:
  - git
---
git commit 을 돌리는 방법 중 reset 과 revert 가 있는데,
이 둘의 차이점을 잘 모르는 상태에서 쓴거 같아서 정리한다.

reset
---
git 의 commit 이력중 원하는 이력으로 '이동' 하는 것.

    $ git reset [옵션] [돌아가고 싶은 커밋해시]

 - 옵션
    1. mixed  
    돌아가려는 커밋 이후의 변경내용은 남아있고, 변경내역은 staged 상태가 아니게 된다. 
    예를 들면, a-b-c 순으로 커밋이 되어 있는 경우, b 커밋으로 mixed 옵션을 써서 돌아간다면($ git reset b // mixed 가 default 라서 옵션명을 안써줘도 됨)
    c 에서 했던 작업은 남아있고, c 의 작업은 unstaged 상태가 된다. 
     
    2. hard  
    돌아가려는 커밋 이후의 내용을 모두 삭제한다.  
    예를 들면, a-b-c 순으로 커밋이 되어 있는 경우, b 커밋으로 hard 옵션을 써서 돌아간다면($ git reset --head b)
    c 에서 했던 작업은 모두 사라진다.
    
    3. soft  
    돌아가려는 커밋 이후의 변경내용은 남아있고, 변경내역은 staged 상태가 된다.  
    예를 들면, a-b-c 순으로 커밋이 되어 있는 경우, b 커밋으로 soft 옵션을 써서 돌아간다면($ git soft --head b)
    c 에서 했던 작업은 남아있고, c 의 작업은 staged 상태가 된다.(commit 직전 상태)

revert
---
git 의 commit 이력중 원하는 이력을 '없었던 것' 으로 만드는 것

    $ git revert [없었던 것으로 하고싶은 커밋해시]
    
revert 는 있었던 일을 없었던 것으로 만들기 때문에 'revert를 한 커밋에 해당되는 내용이 모두 삭제'된다.  
예를 들면 a-b-c 순으로 커밋이 되어 있는 경우, c 의 작업을 revert 하게 되면($ git revert c) c 에서 했던 작업은 모두 사라지고,
      
      Revert "revert test c"
      This reverts commit [없었던 것으로 하고싶은 커밋해시]

위와 같은 커밋 메시지가 남게 된다.


reset 은 reset 을 했다는 커밋 메시지가 따로 안남고, revert 는 따로 남는게 큰 차이인거 같다.  
그리고 이미 push 를 했을때는 revert 를 사용 하는것이 좋다. reset 은 로컬저장소에서만 이력이 돌아가는 것이기 때문에..