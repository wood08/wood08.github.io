---
title: "Day 6: Let's Review"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-review-loop/problem>

    <?php
    $_fp = fopen("php://stdin", "r");
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */
    
    $cnt = 0;
    while(false !== ($_str = fgets($_fp))){
        $cnt++;
        if($cnt == 1){
            continue;
        }
        $even = '';
        $odd = '';
        $_str = trim($_str);
        $str = str_split($_str);
        $chk = strlen($_str);
        for($j=0; $j<count($str); $j++){
            if($j % 2 == 0){
                $even .= $str[$j];
            } else {
                $odd .= $str[$j];
            }
        }
        echo $even.' '.$odd."\n";
    }
    ?>
