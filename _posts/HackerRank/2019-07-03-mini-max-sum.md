---
title: "Mini-Max Sum"
categories:
  - HackerRank
tags:
  - Algorithms
---

<https://www.hackerrank.com/challenges/mini-max-sum/problem>

    <?php
    
    // Complete the miniMaxSum function below.
    function miniMaxSum($arr) {
        sort($arr);
        echo ($arr[0]+$arr[1]+$arr[2]+$arr[3]).' '.($arr[1]+$arr[2]+$arr[3]+$arr[4]);
    }
    
    $stdin = fopen("php://stdin", "r");
    
    fscanf($stdin, "%[^\n]", $arr_temp);
    
    $arr = array_map('intval', preg_split('/ /', $arr_temp, -1, PREG_SPLIT_NO_EMPTY));
    
    miniMaxSum($arr);
    
    fclose($stdin);



배열이 무조건 5개로 들어온다고 해서 저렇게 했는데, 혹시나 해서 포럼 보니 역시나....  
배열을 잘라서 SUM 해도 될꺼같은 그런 느낌적인 기분...