---
title: "Day 2: Operators"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-operators/problem>

	<?php

    // Complete the solve function below.
    function solve($meal_cost, $tip_percent, $tax_percent) {
        $total_cost = $meal_cost;
        $total_cost += $meal_cost * ($tip_percent / 100);
        $total_cost += $meal_cost * ($tax_percent / 100);
        echo round($total_cost);
    }

    $stdin = fopen("php://stdin", "r");

    fscanf($stdin, "%lf\n", $meal_cost);

    fscanf($stdin, "%d\n", $tip_percent);

    fscanf($stdin, "%d\n", $tax_percent);

    solve($meal_cost, $tip_percent, $tax_percent);

    fclose($stdin);
