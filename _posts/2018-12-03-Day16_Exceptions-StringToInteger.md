---
title: "Day 16: Exceptions - String to Integer"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-exceptions-string-to-integer/problem>

	<?php
	$handle = fopen ("php://stdin","r");
	fscanf($handle,"%s",$S);

	try {
        new ReflectionClass('ReflectionClass' . ((int)$S.'' !== $S));
        echo $S;
	} catch (Exception $e) {
        echo "Bad String";
	}

	?>


