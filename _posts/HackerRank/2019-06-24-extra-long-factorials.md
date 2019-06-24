---
title: "Extra Long Factorials"
categories:
  - HackerRank
tags:
  - Algorithms
---

<https://www.hackerrank.com/challenges/extra-long-factorials/problem>

    <?php
    
    // Complete the extraLongFactorials function below.
    function extraLongFactorials($n) {
        if($n <= 1) return 1;
        return bcmul($n, extraLongFactorials($n-1));
    }
    
    $stdin = fopen("php://stdin", "r");
    
    fscanf($stdin, "%d\n", $n);
    
    echo extraLongFactorials($n);
    
    fclose($stdin);


문제에 BigIntegers 를 쓰라고 힌트가 있어서 금방 풀 수 있었다.  
원래라면 $n * extraLongFactorials($n-1) 을 썼을텐데 BigIntegers 에서 bcmul 를 쓰라고 나와 있어서 써보니 되더라.  
php BigIntegers 문서에서도 팩토리얼 예제가 있기도 했고. 

출력때 printf 를 사용하면 결과가 제대로 안나오는 문제가 있는 모양. <https://www.php.net/manual/en/function.bcmul.php#110658>