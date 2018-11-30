---
title: "Day 10: Binary Numbers"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-binary-numbers/problem>

    <?php
    
    $stdin = fopen("php://stdin", "r");
    
    fscanf($stdin, "%d\n", $n);
    
    $binary = 0;
    $bin_cnt = 0;
    $bin_max = 0;
    while($n/2 > 0){
        if( $n/2 > 0 ){
           $binary = $n%2;
        } else {
            $binary = $n/2;
        }
        
        if( $binary == 1 ){
            $bin_cnt++;
        } else {
            $bin_max = $bin_max<$bin_cnt?$bin_cnt:$bin_max;
            $bin_cnt = 0;
        }
    
        $n = floor($n/2);
    }
    
    echo $bin_max<$bin_cnt?$bin_cnt:$bin_max;
    
    fclose($stdin);

    
