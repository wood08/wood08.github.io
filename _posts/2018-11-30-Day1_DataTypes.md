---
title: "Day 1: Data Types"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-data-types/problem>


    // Declare second integer, double, and String variables.
    $cnt = 0;
    while(false !== ($char = fgets($handle))){
        if($cnt == 0){
            echo $i + (int)$char;
            echo "\n";
        }
        if($cnt == 1){
            printf("%.1f", ($d + (float)$char));
            echo "\n";
        }
        if($cnt == 2){
            echo $s.$char;
        }
        $cnt++;
    }
    // Read and save an integer, double, and String to your variables.

    // Print the sum of both integer variables on a new line.

    // Print the sum of the double variables on a new line.

    // Concatenate and print the String variables on a new line
    // The 's' variable above should be printed first.


