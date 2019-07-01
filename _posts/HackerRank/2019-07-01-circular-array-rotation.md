---
title: "Circular Array Rotation"
categories:
  - HackerRank
tags:
  - Algorithms
---

<https://www.hackerrank.com/challenges/circular-array-rotation/problem>

    <?php
    
    // Complete the circularArrayRotation function below.
    function circularArrayRotation($a, $k, $queries) {
        $result = [];
        $qCnt = count($queries);
        $aCnt = count($a);
        $k = ($aCnt>$k ? $k : ($k%$aCnt));
        for($i=0;$i<$qCnt;$i++){
            $idx = $queries[$i] - $k;
            if($idx < 0){
                $idx += $aCnt;
            }
            array_push($result, $a[$idx]);
        }
        return $result;
    }
    
    $fptr = fopen(getenv("OUTPUT_PATH"), "w");
    
    $stdin = fopen("php://stdin", "r");
    
    fscanf($stdin, "%[^\n]", $nkq_temp);
    $nkq = explode(' ', $nkq_temp);
    
    $n = intval($nkq[0]);
    
    $k = intval($nkq[1]);
    
    $q = intval($nkq[2]);
    
    fscanf($stdin, "%[^\n]", $a_temp);
    
    $a = array_map('intval', preg_split('/ /', $a_temp, -1, PREG_SPLIT_NO_EMPTY));
    
    $queries = array();
    
    for ($i = 0; $i < $q; $i++) {
        fscanf($stdin, "%d\n", $queries_item);
        $queries[] = $queries_item;
    }
    
    $result = circularArrayRotation($a, $k, $queries);
    
    fwrite($fptr, implode("\n", $result) . "\n");
    
    fclose($stdin);
    fclose($fptr);


시간 없을꺼 같아서 메일로 온 문제 풀었다.  
한번 슥 생각해서 풀었는데 통과.  
뭔가 더 좋은 방법이 있었을라나...?