---
title: "Day 13: Abstract Classes"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-abstract-classes/problem>

    //Write MyBook class
    class MyBook extends Book {
        protected $price;
            function __construct($t, $a, $p){
            parent::__construct($t, $a);
            $this->price = $p;
        }
    public function display(){
            print('Title: '.$this->title);
            print('Author: '.$this->author);
            print('Price: '.$this->price);
        }
    }