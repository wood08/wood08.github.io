---
title: "Day 9: Recursion 3"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-recursion/problem>

    <?php

    // Complete the factorial function below.
    function factorial($n) {
        if($n == 1){
            return $n;
        } else {
            return $n * factorial($n-1);
        }
    }
    
    $fptr = fopen(getenv("OUTPUT_PATH"), "w");
    
    $stdin = fopen("php://stdin", "r");
    
    fscanf($stdin, "%d\n", $n);
    
    $result = factorial($n);
    
    fwrite($fptr, $result . "\n");
    
    fclose($stdin);
    fclose($fptr);
    
