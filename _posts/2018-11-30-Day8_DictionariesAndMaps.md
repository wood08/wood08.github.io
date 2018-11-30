---
title: "Day 8: Dictionaries and Maps"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-dictionaries-and-maps/problem>

    <?php
    $_fp = fopen("php://stdin", "r");
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */
    $cnt = trim(fgets($_fp));
    
    $arr = [];
    for($i=0;$i<$cnt;$i++){
        $str = explode(' ', trim(fgets($_fp)));
        $arr[$str[0]] = $str[1];
    }
    
    while(false !== ($str = fgets($_fp))){
        $str = trim($str);
        if(isset($arr[$str])){
            echo $str.'='.$arr[$str]."\n";
        } else {
            echo "Not found\n";
        }
    }
    
    ?>
