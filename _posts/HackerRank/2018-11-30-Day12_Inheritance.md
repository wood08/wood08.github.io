---
title: "Day 12: Inheritance"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-inheritance/problem>

    class Student extends person {
        private $testScores;
        /*
        *   Class Constructor
        *
        *   Parameters:
        *   firstName - A string denoting the Person's first name.
        *   lastName - A string denoting the Person's last name.
        *   id - An integer denoting the Person's ID number.
        *   scores - An array of integers denoting the Person's test scores.
        */
        // Write your constructor here
        public $first_name, $last_name, $id, $scores;
        function __construct($_first_name, $_last_name, $_id, $_scores){
            $this->first_name = $_first_name;
            $this->last_name = $_last_name;
            $this->id = $_id;
            $this->scores = $_scores;
        }

        function printPerson(){
            print("Name: ".$this->last_name.", ".$this->first_name."\n");
            print("ID: ".$this->id."\n");
        }

        /*
        *   Function Name: calculate
        *   Return: A character denoting the grade.
        */
        // Write your function here
        private $grade = ['O', 'E', 'A', 'P', 'D', 'T'];
        private $grade_score = [90, 80, 70, 55, 40, 0];
        function calculate(){
            $scores = $this->scores;
            $ever = 0;
            for($i=0; $i<count($scores); $i++){
                $ever+=$scores[$i];
            }
            $ever = $ever / count($scores);
            for($i=0; $i<count($this->grade); $i++){
                if($ever >= $this->grade_score[$i]){
                    return $this->grade[$i];
                }
            }
        }
    }





