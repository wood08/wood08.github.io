---
title: "Day 3: Intro to Conditional Statements"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-operators/problem>

	<?php
    $stdin = fopen("php://stdin", "r");
    
    fscanf($stdin, "%d\n", $N);
    
    // If  is odd, print Weird
    if($N % 2 == 1){
        print('Weird');
    } else if($N >= 2 && $N <= 5){
        // If  is even and in the inclusive range of 2 to 5, print Not Weird
        print('Not Weird');
    } else if($N >= 6 && $N <= 20){
        // If  is even and in the inclusive range of 6 to 20, print Weird
        print('Weird');
    } else {
        // If  is even and greater than 20, print Not Weird
        print('Not Weird');
    }
    
    fclose($stdin);

