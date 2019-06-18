---
title: "Climbing the Leaderboard"
categories:
  - HackerRank
tags:
  - Algorithms
---

<https://www.hackerrank.com/challenges/climbing-the-leaderboard/problem>

    <?php
    
    // Complete the climbingLeaderboard function below.
    function climbingLeaderboard($scores, $alice) {
        $result = [];
        $scores = array_unique($scores, SORT_NUMERIC);
        rsort($scores);
        $rank = count($scores)-1;
    
        foreach($alice as $v){
            while($rank >= 0){
                if($rank > count($scores)-1){
                    $rank = count($scores)-1;
                }
                if($v >= $scores[$rank]){
                    $rank--;
                } else {
                    $rank = $rank+2;
                    break;
                }
            }
            if($rank < 0){
                $rank = 1;
            }
            array_push($result, $rank);
        }
        return $result;
    }
    
    $fptr = fopen(getenv("OUTPUT_PATH"), "w");
    
    $stdin = fopen("php://stdin", "r");
    
    fscanf($stdin, "%d\n", $scores_count);
    
    fscanf($stdin, "%[^\n]", $scores_temp);
    
    $scores = array_map('intval', preg_split('/ /', $scores_temp, -1, PREG_SPLIT_NO_EMPTY));
    
    fscanf($stdin, "%d\n", $alice_count);
    
    fscanf($stdin, "%[^\n]", $alice_temp);
    
    $alice = array_map('intval', preg_split('/ /', $alice_temp, -1, PREG_SPLIT_NO_EMPTY));
    
    $result = climbingLeaderboard($scores, $alice);
    
    fwrite($fptr, implode("\n", $result) . "\n");
    
    fclose($stdin);
    fclose($fptr);


처음에 짰을때는 대용랑 자료에 관해서는 타임아웃이 나와서 어떻게 해야하나 고민했는데, 이 문제에서 핵심은 앨리스의 점수는 점점 올라가는 것인듯.  
앨리스의 새 점수를 받을때마다 꼭 처음부터 등수 계산을 할 필요가 없다는 것.
