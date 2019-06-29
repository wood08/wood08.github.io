---
title: "Time Conversion"
categories:
  - HackerRank
tags:
  - Algorithms
---

<https://www.hackerrank.com/challenges/time-conversion/problem>

    <?php
    
    /*
     * Complete the timeConversion function below.
     */
    function timeConversion($s) {
        $s_arr = explode(':', $s);
        $s_last = str_split($s_arr[2],2);
        $s_arr[2] = $s_last[0];
        if($s_last[1] == 'PM'){
            if($s_arr[0] != '12'){
                $s_arr[0] = ((int)$s_arr[0])+12;
            }
        } else if($s_arr[0] == '12'){
            $s_arr[0] = '00';
        }
    
        return $s_arr[0].":".$s_arr[1].":".$s_arr[2];
    }
    
    $fptr = fopen(getenv("OUTPUT_PATH"), "w");
    
    $__fp = fopen("php://stdin", "r");
    
    fscanf($__fp, "%[^\n]", $s);
    
    $result = timeConversion($s);
    
    fwrite($fptr, $result . "\n");
    
    fclose($__fp);
    fclose($fptr);



쉬어가는 날.  
보통 알고리즘 문제풀다보면, 웹플밍에서는 쓰기에 좀 애매해보이는 어려운 것들이 많이 나오는데, 이건 실제로도 써먹을 일이 있지 않을까? 하는 문제였다.  
요 몇일 좀 바빠서 문제 못풀다보니 머리 다시 재가동할 겸 쉬엄쉬엄... 