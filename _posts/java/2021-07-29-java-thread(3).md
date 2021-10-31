---
layout: post
current: post
cover: assets/built/images/java/cover/cover_java.png
navigation: True
title: 쓰레드 정리 (3) 
date: 2021-07-29 00:14:00
tags: [java]
class: post-template
subclass: 'post'
author: nageom
---
<h6> 첫번째 알아볼 쓰레드 정의는 </h6>
쓰레드는 우선순위(priority)이다. 

> 쓰레드의 우선순위

쓰레드는 우선순위(priority)라는 멤버변수를 가지고 있어 ,이 우선순위의 값에 따라
쓰레드가 얻는 실행시간이 달라진다. <br>
어떨 때 쓰느냐하면 
카톡을 사용할때 파일 다운로드를 처리하는 쓰레드보다 채팅내용을 전송하는 쓰레드의 우선순위가 더 높아야 
사용자가 채팅하는데 불편함이 없을 것이다. 대신 파일다운로드 작업에 걸리는 시간은 더 길어질테지만,
이러한 작업의 중요도에 따라 쓰레드의 우선순위를 서로 다르게 지정하여 특정 쓰레드가 더 많은 작업시간을 갖도록 하는 것이 
우선순위의 용도이다. <br>


**쓰레드의 우선순위 지정하기** <br>
void setPriority(int newPriority) //쓰레드의 우선순위를 지정한 값으로 변경한다.<br>
int getPriority() //쓰레드의 우선순위를 반환한다.<br>

1. 우선순위의 범위는 1~10이며 숫자가 높을수록 우선순위가 높다. <br>
2. 쓰레드의 우선순위는 쓰레드를 생성한 쓰레드로부터 상속받는다. <br>
main메서드를 수행하는 쓰레드는 우선순위가 5이므로 main메서드내에서 생성하는 쓰레드의 우선순위는 자동적으로 5가 된다. <br>

예제
<script src="https://gist.github.com/nageom/6245e8f2c3c6359706127c8607187d0e.js"></script>

결과
![ex_screenshot](../../assets/built/images/java/thread/thread(3)_priority.png) 
main쓰레드의 우선순위 5를 상속받은 th1과 th2 중,
th2만 우선순위를 7로 변경한 다음 start()를 호출해서 쓰레드를 실행시켰다. 
결과를 보면 우선순위가 높은 th2의 실행시간이 th1에 비해 늘고 더 우선시 되었다는것을 알 수 있다.

![ex_screenshot](../../assets/built/images/java/thread/thread(3)_priority2.png)
빨간 t1,t2은 실행이 끝난 시점을 나타냄

위의 발로 그린 그림은 싱글 코어로 두 개의 쓰레드로 두개의 작업을 실행했을 때의 
결과를 그림으로 나타낸 것인데,
우선순위가 같은 경우 각 쓰레드에게 거의 같은 양의 실행시간이 주어지지만, 
우선순위가 다르다면 우선순위가 높은 th2에게 상대적으로 th1보다 더 많은 양의 실행시간이 주어지고
결과적으로 작업 A가 B보다 더 빨리 완료될 수 있다. 
싱글코어에서는 이렇다. <br>

그러나 멀티코어에서는 쓰레드의 우선순위에 따른 차이가
전혀 없었다. 완전 한번씩 돌아가며 실행됐다. 
결국 멀티코어에서는 쓰레드에 높은 우선순위로 실행시간과 실행기회를 줄 수 없다는 것이다. <br>

멀티코어라 해도 OS마다 다른 방식으로 스케쥴링하기 때문에, 어떤 OS에서 실행하느냐에 따라
다른 결과를 얻을 수 있어 굳이 우선순위에 차등을 두어 쓰레드를 실행하려면 특정 OS의 스케쥴링 정책과
JVM의 구현을 직접 확인해봐야 한다. 
만일 확인한다 하더라도 어느 정도 예측만 가능하지 정확히 알 수는 없어,
차라리 쓰레드에 우선순위를 부여하는 대신 작업에 우선순위를 두어 PriorityQueue에 저장해두고,
우선순위가 높은 작업에 먼저 처리되도록 하는 것이 나을것이라 한다. 

<h6>두번째는 쓰레드의 또 다른 유형인 </h6> 

> 데몬 쓰레드(daemon thread)

데몬 쓰레드는 다른 일반 쓰레드의 작업을 돕는 보조적인 역할을 수행하는 쓰레드이다 
일반 쓰레드가 모두 종료되면 데몬 쓰레드는 강제적으로 자동 종료되는데, 그 이유는 앞서 말했듯이
일반 쓰레드의 보조역할을 수행하기 때문이다. 

데몬 쓰레드의 예로는 가비지 컬렉터, 워드프로세서의 자동저장, 화면자동갱신 등이 있다. 

데몬 쓰레드는 <U>무한루프와 조건문을 이용해서 실행 후 대기하고 있다가 특정 조건이 만족되면 작업을 수행하고 
다시 대기하도록 작성한다.</U>

데몬 쓰레드를 만들어볼건데, 일단 일반 쓰레드 생성와 동일하게 생성하고 실행전에 setDaemon(true)를 호출한다.<br>
boolean isDaemon() //데몬 쓰레드인지 확인 <br>
void setDaemon(boolean on) //쓰레드를 데몬쓰레드로 변경 <br>
//on의 값을 true로 지정해야함. <br>

![ex_screenshot](../../assets/built/images/java/thread/thread(3)_priority3.png)

3초마다 변수 autoSave의 값을 확인해서 그 값이 true이면 autoSave()를 호출하는 일을 무한히
반복하도록 쓰레드를 작성했다.
무한 반복임에도 프로그램은 종료되었다. 

만일 setDaemon메서드를 호출하지 않은 일반 쓰레드라면 강제종료를 하지 않는 이상 종료되지 않을 것이다.
![ex_screenshot](../../assets/built/images/java/thread/thread(3)_priority4.png)

신기신기

<h6>세번째는 </h6>
> 쓰레드 그룹(thread group)

쓰레드 그룹은 서로 관련된 쓰레드를 그룹으로 다루기 위한 것으로,
폴더를 생성해서 관련된 파일들을 함께 넣어서 관리하는 것처럼 그룹을 생성해서 쓰레드를 구룹으로 묶어서 
관리할 수 있다. 
또한 폴더 안에 폴더생성이 가능하듯이 쓰레드 그룹에 다른 쓰레드 그룹을 포함 시킬 수 있다.
쓰레드 그룹은 보안상의 이유로 도입되어 자신이 속한 쓰레드 그룹이나 하위 쓰레드 그룹은 변경 가능하지만
다른 쓰레드 그룹의 쓰레드는 변경 불가능.

<U>쓰레드 그룹에서 알아둘 점</U><br>
* 모든 쓰레드는 반드시 그룹에 포함되어 있어야한다.
* 자바 어플리케이션이 실행되면, JVM은 main과 system이라는 쓰레드 그룹을 만들고
JVM운영에 필요한 쓰레드들을 생성해서 이 쓰레드 그룹에 포함시킨다. 
* 우리가 생성한 모든 쓰레드 그룹은 MAIN쓰레드 그룹의 하위 쓰레드 그룹이 되며,
그룹을 지정하지 않은 쓰레드는 자동으로 main쓰레드 그룹에 속하게 된다. 

쓰레드를 쓰레드 그룹에 포함시키려면 Thread의 생성자를 이용한다.
Thread(ThreadGroup group, Runnable target, String name)

**기본 쓰레드 그룹 생성, 지정 예시**
~~~ javascript
//main 안에서
ThreadGroup grp1 = new ThreadGroup("Group1");//쓰레드 그룹 생성

Runnable r = new Runnable() {
    public void run() {
        try {
            Thread.sleep(1000);
           }catch(InterruptedException e) {}
        }
    }
};

//Thread(ThreadGourp tg, Runnable r, String name)
new Thread(grp1, r, "th1").start(); //쓰레드 그룹 포함 & 실행

main.list();
// 이 메서드로 main쓰레드 그룹의 정보를 출력한다. 

~~~


참고문서 - 자바의 정석






 
