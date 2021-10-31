---
layout: post
current: post
cover: assets/built/images/java/cover/cover_java.png
navigation: True
title: 쓰레드-동기화(Synchronization) (4) 
date: 2021-08-05 00:14:00
tags: [java]
class: post-template
subclass: 'post'
author: nageom
---
오늘은 <U>'사용해본적은 있지만 자세히는 모른다 시리즈'</U>의 synchronized에 대해 포스팅해보려한다. 가보자<br>

한 쓰레드가 진행 중인 작업을 다른 쓰레드가 간섭하지 못하도록 막는 것을 '쓰레드의 동기화 (synchronization)'라고 한다.

알다시피 싱글 쓰레드와 다르게 멀티 쓰레드는 여러 쓰레드들이 같은 프로세스 내의 자원을 공유해 작업하기 때문에
서로의 작업에 영향이 갈 수 밖에 없다. 
A 쓰레드가 작업 중 B쓰레드가 공유자원을 임의로 변경한다면,
A 쓰레드가 작업을 마쳤을 때 원래 의도했던 것과는 다른 결과를 얻을 수 있다. 
이러한 일의 방지를 위해 도입된 개념이 '임계 영역(CRITICAL SECTION)'과 '잠금(LOCK)'이다. <br>

**'임계 영역(CRITICAL SECTION)'과 '잠금(LOCK)'**
공유 데이터를 사용하는 코드 영역을 임계 영역으로 지정하고, 
공유 데이터(객체)가 가지고 있는 lock을 획득한 단 하나의 쓰레드만 이 영역 내의 코드를 수행할 수 있게 한다 .
그리고 해당 쓰레드가 임계 영역 내의 모든 코드를 수행하고 벗어나서 lock을 반납해야만
다른 쓰레드가 반납된 lock을 획득하여 임계 영역의 코드를 수행할 수 있게 된다. <br>

(JDK1.5 이후
java.util.concurrent.locks / 
java.util.concurrent.atomic 패키지 지원 )<br>

임계 영역을 지정하는데는 두 가지 방법이 있다.
~~~ javascript
//1. 메서드 전체를 지정
public synchronized void aa(){
    //..
}
/* 쓰레드는 synchronized메서드가 호출된 시점부터 해당 메서드가 포함된 객체의 lock을 얻어 작업을 수행하며
메서드가 종료되면 lock을 반환한다. 



*/
//2. 특정한 영역을 지정
synchronized ( 객체의 참조변수) {}
/*
메서드 내의 코드 일부를 블럭{}으로 감싸고 블럽 앞에 synchronized(참조변수)를 붙이는 것으로 
이때의 참조변수는 락을 걸고자하는 객체를 참조하는 것이어야 한다 

*/
~~~
이 두 방법 모두 lock의 획득과 반납이 모두 자동적으로 이루어진다. 
참고로 synchronized블럭으로 임계 영역을 최소화해서 보다 효율적인 프로그램이 되도록 노력하는 것이 좋다. 

출금하려는 금액이 잔고보다 작을 경우에만 출금할 수 있는 은행시스템에서 필요한 쓰레드 동기화
<script src="https://gist.github.com/nageom/ba97d73b55ce060e79fb91dedc72723d.js"></script>

24 줄의 메서드를 동기화하지 않으면 한 쓰레드가 출금 중, 다른 쓰레드가 balance에 영향을 줘서
balance가 음수가 되어버린다. <synchronized 를 지우고 결과를 확인해보자>

> 알게된것

위의 예제에서 쓰레드들이 구현될때 account 객체를 따로 생성해 가지고 있을거라 생각하고
동기화 없이도 balance가 음수가 되지않을거라고 예상했고 이는 틀렸다. 

내가 만든 RunnableEx 안의 멤버 또는 메서드들은 모두
메인에서 구현된 쓰레드들이 같이 공유한다. 라는걸 기억해두자. 




참고문서 - 자바의 정석






 
