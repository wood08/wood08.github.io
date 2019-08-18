---
title: create 와 save(insert)
categories:
  - laravel
tags:
  - laravel, ORM
---
라라벨에서 데이터를 생성(입력)하는 방법으로 대표적으로 두가지 방법이 있다.
1. create
2. save(insert)

create 를 사용하여 한줄로 데이터를 입력할 수 있지만, 이 경우에는 fillable 이나 guarded 속성을 지정해줘야한다. 지정해주지 않을 경우 악의적인 사용자로 인해, 원하지 않은 필드에 값을 입력할 될 수 있기 때문이다.(말하자면 공격방지)  
fillable 은 사용할 필드명을 지정(화이트리스트), guarded 는 사용하지 않을 필드명을 지정(블랙리스트) 하는 것이다.  
두가지는 같이 사용될 수 없다.

자세한 내용은 다음 링크 확인
<https://laravel.kr/docs/5.8/eloquent#mass-assignment>

그 외에 데이터 생성 방법으로는
firstOrCreate, firstOrNew, updateOrCreate 가 있다.
firstOrNew 는 save 를 해줘야지 저장된다.
<https://laravel.kr/docs/5.8/eloquent#other-creation-methods>