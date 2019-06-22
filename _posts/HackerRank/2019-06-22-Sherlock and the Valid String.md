---
title: "Sherlock and the Valid String"
categories:
  - HackerRank
tags:
  - Algorithms
---

<https://www.hackerrank.com/challenges/sherlock-and-valid-string/problem>

    <?php
    
    // Complete the isValid function below.
    function isValid($s) {
        $s = str_split($s);
        $array = [0,0,0,0,0,0,0,0,0,0,
            0,0,0,0,0,0,0,0,0,0,
            0,0,0,0,0,0];
        $char_cnt = 0;
        for($i=0;$i<count($s);$i++){
            $ord = ord($s[$i])-97;
            if($array[$ord]==0) $char_cnt++;
            $array[$ord]++;
        }
    
        $arr = array_filter($array);
        $max = max($arr);
        $min = min($arr);
    
        if($max==$min) return 'YES';
    
        $max_cnt = 0;
        $min_cnt = 0;
        $other_cnt = 0;
        foreach($arr as $v){
            if($v == $max) $max_cnt++;
            if($v == $min) $min_cnt++;
            if($v != $min && $v != $max) $other_cnt++;
        }
    
        if($other_cnt > 0) return 'NO';
        if($max-$min == 1 && $max_cnt==1) return 'YES';
        if($min == 1 && $min_cnt==1) return 'YES';
    
        return 'NO';
    }
    
    $fptr = fopen(getenv("OUTPUT_PATH"), "w");
    
    $stdin = fopen("php://stdin", "r");
    
    $s = '';
    fscanf($stdin, "%[^\n]", $s);
    
    $result = isValid($s);
    
    fwrite($fptr, $result . "\n");
    
    fclose($stdin);
    fclose($fptr);


문자열 안에 모든 문자가 같은 횟수만큼 나오면 유효한 문자열.  
aabbcc => 유효한 문자열  
aabbbcccd => 유효하지 않은 문자열

단, 1개 정도는 문자열이 많아도 삭제 가능하다.  
aabbccc => c 하나를 삭제하면 유효한 문자열이 됨  
aabbcccc => c 하나를 삭제해도 유효하지 않음

'문자열의 문자갯수가 모두 같은가?' 의 확인 까지는 간단한데, 문자 한개를 삭제 가능하다는 것 때문에 좀 시간이 걸렸다.  
좀 더 이쁘게 짤 수 없나? 고민하게 되는 소스...
