---
title: "Day 23: BST Level-Order Traversal"
categories:
  - HackerRank
tags:
  - 30DaysOfCode
---

<https://www.hackerrank.com/challenges/30-binary-trees/problem>

    <?php
    class Node{
        public $left,$right;
        public $data;
        function __construct($data)
        {
            $this->left=$this->right=null;
            $this->data = $data;
        }
    }
    class Solution{
        public function insert($root,$data){
            if($root==null){
                return new Node($data);
            }
            else{
                if($data<=$root->data){
                    $cur=$this->insert($root->left,$data);
                    $root->left=$cur;
                }
                else{
                    $cur=$this->insert($root->right,$data);
                    $root->right=$cur;
                }
                return $root;
            }
        }

        public function levelOrder($root){
            //Write your code here
            $arr = array();

            $arr[] = $root;
            while(!empty($arr)) {
                $node = array_shift($arr);
                if(!empty($node->left)) {
                    $arr[] = $node->left;
                }
                if(!empty($node->right)) {
                    $arr[] = $node->right;
                }
                echo $node->data." ";
            }
        }

    }//End of Solution
    $myTree=new Solution();
    $root=null;
    $T=intval(fgets(STDIN));
    while($T-->0){
        $data=intval(fgets(STDIN));
        $root=$myTree->insert($root,$data);
    }
    $myTree->levelOrder($root);
    ?>
