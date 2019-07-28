---
title: "Beautiful Days at the Movies"
categories:
  - HackerRank
tags:
  - Algorithms
---

<https://www.hackerrank.com/challenges/beautiful-days-at-the-movies/problem>

    <?php
    
    // Complete the beautifulDays function below.
    function beautifulDays($i, $j, $k) {
        $result = 0;
        for($i; $i<=$j;$i++){
            $num1 = (string)$i;
            $num2 = strrev($num1);
    
            $chk = (abs((int)$num1 - (int)$num2)) % $k;
            if(!$chk){
                $result++;
            }
        }
        return $result;
    }
    
    $fptr = fopen(getenv("OUTPUT_PATH"), "w");
    
    $stdin = fopen("php://stdin", "r");
    
    fscanf($stdin, "%[^\n]", $ijk_temp);
    $ijk = explode(' ', $ijk_temp);
    
    $i = intval($ijk[0]);
    
    $j = intval($ijk[1]);
    
    $k = intval($ijk[2]);
    
    $result = beautifulDays($i, $j, $k);
    
    fwrite($fptr, $result . "\n");
    
    fclose($stdin);
    fclose($fptr);



솔직히 문제가 넘 쉬워서 그런가. 영어도 쉬웠다. 번역기 한번 돌렸긴 하지만...