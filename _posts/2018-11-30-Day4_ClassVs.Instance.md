---
title: "Day 4: Class vs. Instance"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-class-vs-instance/problem>

	<?php
	class Person{
		public $age;
	    public function __construct($initialAge){
          // Add some more code to run some checks on initialAge
          if($initialAge<0){
              echo "Age is not valid, setting age to 0.\n";
              $initialAge = 0;
          }
          $this->age = $initialAge;

		}
	    public  function amIOld(){
            // Do some computations in here and print out the correct statement to the console 
            if($this->age<13){
                echo "You are young.\n";
            } else if($this->age>= 13 && $this->age<18){
                echo "You are a teenager.\n";
            } else {
                echo "You are old.\n";
            }

		}
	    public  function yearPasses(){
            // Increment the age of the person in here
            $this->age++;
        }
	}