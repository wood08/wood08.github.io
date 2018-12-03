---
title: "Day 15: Linked List"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-linked-list/problem>

	<?php
	class Node{
        public $data;
        public $next;
        function __construct($d)
        {
            $this->data = $d;
            $this->next = NULL;
        }
	}
	class Solution{
        function insert($head,$data){
            $node = new Node($data);
            
            if($head == null) {
                $head = $node;
            } else if ($head->next == null) {
                $head->next = $node;
            } else {
                $start = $head;
                while($start->next != null) {
                    $start = $start->next;
                }
                $start->next = $node;
            }
            return $head;
        }

	function display($head){
        $start=$head;
            while($start){
                echo $start->data,' ';
                $start=$start->next;
            }
        }
	}
	$T=intval(fgets(STDIN));
	$head=null;
	$mylist=new Solution();
	while($T-->0){
        $data=intval(fgets(STDIN));
        $head=$mylist->insert($head,$data);
	}
	$mylist->display($head);
	?>


