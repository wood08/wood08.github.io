---
title: "Day 25: Running Time and Complexity"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-running-time-and-complexity/problem>

    <?php
    $_fp = fopen("php://stdin", "r");
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */
    
    fscanf($_fp, "%d\n", $n);
    for($i=0;$i<$n;$i++){
        fscanf($_fp, "%d\n", $num);
        $prime_chk = 0;
        if($num==1){
            echo "Not prime\n";
            continue;
        }
        for($j=2;$j*$j<=$num;$j++){
            if($num%$j==0){
                echo "Not prime\n";
                $prime_chk = 1;
                break;
            }
        }
        if($prime_chk==0){
            echo "Prime\n";
        }
    }
    
    fclose($_fp);
    ?>
    




