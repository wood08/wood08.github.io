---
title: "Save the Prisoner!"
categories:
  - HackerRank
tags:
  - Algorithms
---

<https://www.hackerrank.com/challenges/save-the-prisoner/problem>

    <?php
    
    // Complete the saveThePrisoner function below.
    function saveThePrisoner($n, $m, $s) {
        $result = ($m + ($s - 1) % $n);
        $result = $result % $n;
        return $result == 0 ? $n : $result;
    }
    
    $fptr = fopen(getenv("OUTPUT_PATH"), "w");
    
    $stdin = fopen("php://stdin", "r");
    
    fscanf($stdin, "%d\n", $t);
    
    for ($t_itr = 0; $t_itr < $t; $t_itr++) {
        fscanf($stdin, "%[^\n]", $nms_temp);
        $nms = explode(' ', $nms_temp);
    
        $n = intval($nms[0]);
    
        $m = intval($nms[1]);
    
        $s = intval($nms[2]);
    
        $result = saveThePrisoner($n, $m, $s);
    
        fwrite($fptr, $result . "\n");
    }
    
    fclose($stdin);
    fclose($fptr);


영어 공부합시다!!!!