---
title: "비트나미-아파치 서버 루트폴더 변경하기"
categories:
  - Server
tags:
  - Server Bitnami
---
phpStorm 으로 조금씩 연습해보고 있는데, alt+F2키를 눌러서 php 실행시켰을때 가끔 502 에러가 뜨는 문제가 발생.

찾아보니까 phpStorm 내부에서 실행할때 나는 문제라고 한다. 제대로 웹서버를 사용하면 나지 않는 문제라고...

웹서버는 이미 비트나미로 아파치가 깔려있어서 이걸 사용하기로 함.

apache2/conf/httpd.conf 파일에서 다음과 같이 디렉토리 루트를 수정했는데

    DocumentRoot "D:/GitHub"
    <Directory "D:/GitHub">
    
제대로 안됨. 아무리해도 비트나미 index.html 을 못벗어남.

비트나미로 깐거라서 그런지 apache2/conf/bitnami/bitnami.conf 파일도 같이 수정해줘야 했다.

bitnami.conf 파일도 수정해주니 정상 작동.
