---
title: "Larry's Array"
categories:
  - HackerRank
tags:
  - Algorithms
---

<https://www.hackerrank.com/challenges/larrys-array/problem>

    <?php
    
    // Complete the larrysArray function below.
    function larrysArray($A) {
        $cnt = 0;
        for($i=0;$i<count($A)-1;$i++){
            for($j=$i+1;$j<count($A);$j++){
                if($A[$i]>$A[$j]){
                    $cnt++;
                }
            }
        }
        echo 'cnt='.$cnt;
        return $cnt % 2 == 0 ? 'YES' : 'NO';
    }
    
    $fptr = fopen(getenv("OUTPUT_PATH"), "w");
    
    $stdin = fopen("php://stdin", "r");
    
    fscanf($stdin, "%d\n", $t);
    
    for ($t_itr = 0; $t_itr < $t; $t_itr++) {
        fscanf($stdin, "%d\n", $n);
    
        fscanf($stdin, "%[^\n]", $A_temp);
    
        $A = array_map('intval', preg_split('/ /', $A_temp, -1, PREG_SPLIT_NO_EMPTY));
    
        $result = larrysArray($A);
    
        fwrite($fptr, $result . "\n");
    }
    
    fclose($stdin);
    fclose($fptr);


못푸는줄 알았다. 토론쪽에 15퍼즐을 봐보라고 하는말 없었으면 못풀뻔;;  

[15퍼즐 분석 설명](http://blog.naver.com/PostView.nhn?blogId=sctivcrmnfe&logNo=220906129519)

숫자가 이동하는 횟수의 총 합이 홀수인 경우에는 정렬할 수 없다. 숫자가 이동할때는 짝수값만큼의 변화가 생기기 때문. 이 핵심.

하면서 버블정렬 알고리즘도 짜보고 난리쳤었는데...ㅠㅠ

그럼 15가 아닌 8 이나 24 퍼즐 같은 경우에는 어떻게 되는 것인지?
 
위 블로그에서 나온대로 이동시 차이값 계산해보니  
8퍼즐:S=0, 1, 3  
24퍼즐:S=0, 3, 5  
=> 홀수증가

만약 숫자의 위치를 맞출 수 없도록 일부러 바꾼 경우에는 S값은 짝수.  
퍼즐이 모두 맞춰줬을때 S 값은 각각 3과 5라서 맞출 수 없음.  
==> 이 경우 홀수값이 나올 경우에는 OK 인 것인가?  

퍼즐 사오고 싶다 ㅋㅋㅋ