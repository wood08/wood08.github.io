---
title: "Designer PDF Viewer"
categories:
  - HackerRank
tags:
  - Algorithms
---

<https://www.hackerrank.com/challenges/designer-pdf-viewer/problem>

    <?php
    
    // Complete the designerPdfViewer function below.
    function designerPdfViewer($h, $word) {
        $word = str_split($word);
        $height = 0;
        $wide = count($word);
        for($i=0;$i<$wide;$i++){
            $tmp = $h[(ord($word[$i])-97)];
            if( $height < $tmp ){
                $height = $tmp;
            }
        }
        
        return $height * $wide;
    }
    
    $fptr = fopen(getenv("OUTPUT_PATH"), "w");
    
    $stdin = fopen("php://stdin", "r");
    
    fscanf($stdin, "%[^\n]", $h_temp);
    
    $h = array_map('intval', preg_split('/ /', $h_temp, -1, PREG_SPLIT_NO_EMPTY));
    
    $word = '';
    fscanf($stdin, "%[^\n]", $word);
    
    $result = designerPdfViewer($h, $word);
    
    fwrite($fptr, $result . "\n");
    
    fclose($stdin);
    fclose($fptr);


easy 레벨은 알고리즘 보다 독해가 문제인듯...