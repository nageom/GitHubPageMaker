---
layout: post
current: post
cover: assets/built/images/java/cover/cover_java1.8.png
navigation: True
title: 자바 1.8버전 차이를 알아보자
date: 2021-06-18 00:14:00
tags: [java]
class: post-template
subclass: 'post'
author: nageom
---
***
> 요즘은 자바의 정석이라는 책으로 공부중인데 읽다보면 중간중간 JDK 버전 상승에 따라 바뀐 기능에 대해서도
> 조금씩 나온다. 사실 면접질문에서도 나왔는데 대답을 하지 못한게 한이 맺혀서.. 책에 나올때마다 포스팅 하려합니다. 

**1) 멀티 catch블럭**<br>

JDK1.7부터 여러 catch블럭을 '|' 기호를 이용해서, 하나의 catch블럭로 합칠 수 있게 되었고, 이를 '멀티 catch블럭'이라한다. <br>
~~~javascript
//본래 사용법
try {
    ...
}catch (ExceptionA e) {
    e.printStackTrace();
}catch (ExceptionB e2){
    e2.printStackTrace();
}
//변경후 멀티 catch블럭
try {
    ...
}catch (ExceptionA | ExceptionB e) {
    e.printStackTrace();
}

~~~
중복된 코드를 줄일 수 있는 큰 장점이 있는데<br>
멀티 catch블럭을 사용할 때 지켜줘야하는 것이 있다.<br>
바로 '|' 기호로 연결된 예외 클래스가 조상과 자손의 관계에 있다면 컴파일 에러가 발생한다는것, <br>
왜냐하면, 두 예외 클래스가 조상과 자손의 관계에 있다면, 그것은 조상 클래스만 써주는 것과 똑같기 때문이다. <br>
불필요한 코드는 제거하라는 의미에서 에러가 발생한다. <br>
~~~javascript
try {
    ...
}catch (ParentException | ChildException e){
    e.printStackTrace();//에러가 난다. 
}

~~~
그리고 멀티 catch는 하나의 catch블럭으로 여러 예외를 처리하는 것이기 때문에,<br>
멀티 catch 블럭 내에서는 실제로 어떤 예외가 발생한 것인지 알 수 없다. <br>
그래서 연결된 예외 클래스들의 공통 분모인 조상 예외 클래스에 선언된 멤버만을 사용할 수 있다. <br>
필요하다면 이러한 코드로 어떤 에러가 발생한 것인지 확인 할 수 있다. <br>
~~~ javascript
try {
...
}catch (ExceptionA | ExceptionB e) {
    e.methodA(); //에러 -> Exception A에서 선언된 methodA() 는 호출불가 
    
    if (e instanceof ExceptionA) {
        ExceptionA e1 = (ExceptionA) e;
        e1.methodA(); // 호출 가능
    } else {
    ..
    }
    e.printStackTrace();
}
~~~

**2. 상수와 리터럴 (constant & literal)**<br>
본래 상수 <br>
    final int MAX_SPEED = 10; <br>
   은 반드시 선언과 동시에 초기화해야 하며, 그 후 부터는 상수의 값을 변경하는 것이 허용되지 않는다. <br>
   final int MAX_SPEED ; //에러<br>
   final int MAX_VALUE = 100; // OK<br>
   <br>
현재는 JDK1.6부터 상수를 선언과 동시에 초기화 하지 않아도 되며, 사용하기 전에만 초기화하면 되도록 바뀌었다. <br>
하지만 상수는 성언과 동시에 초기화하는 습관을 들이는 것이 좋다고 한다. _2021-06-21<br>