---
title: "Day 19: Interfaces"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-interfaces/problem>

	<?php
    interface AdvancedArithmetic{
        public function divisorSum($n);
    }

    /*
     * Write your code here
     */
    class Calculator implements AdvancedArithmetic {
        function divisorSum($n) {
            $result = 0;
            for($i=1;$i<=$n;$i++){
                if($n%$i == 0){
                    $result += $i;
                }
            }
            return $result;
        }
    }

    $n=intval(fgets(STDIN));
    $myCalculator=new Calculator();
    if($myCalculator instanceof AdvancedArithmetic)//checking if Calculator has implemented AdvancedArithemtic
    {
        $sum=$myCalculator->divisorSum($n);
        echo "I implemented: AdvancedArithmetic\n".$sum;
    }
    else
    {
        echo "Wrong answer";// You will get this output if you dont implement
    }
    ?>


