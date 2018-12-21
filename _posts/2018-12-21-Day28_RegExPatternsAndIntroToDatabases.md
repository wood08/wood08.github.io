---
title: "Day 28: RegEx, Patterns, and Intro to Databases"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-regex-patterns/problem>

	<?php
    $stdin = fopen("php://stdin", "r");

    fscanf($stdin, "%d\n", $N);

    $arr = [];
    $cnt = 0;
    for ($N_itr = 0; $N_itr < $N; $N_itr++) {
        fscanf($stdin, "%[^\n]", $firstNameEmailID_temp);
        $firstNameEmailID = explode(' ', $firstNameEmailID_temp);

        $firstName = $firstNameEmailID[0];

        $emailID = $firstNameEmailID[1];

        $email = explode('@', $emailID);

        if($email[1] == 'gmail.com'){
            $arr[$cnt] = $firstName;
            $cnt++;
        }
    }

    sort($arr);
    for($i=0; $i<count($arr); $i++){
        echo $arr[$i]."\n";
    }

    fclose($stdin);

