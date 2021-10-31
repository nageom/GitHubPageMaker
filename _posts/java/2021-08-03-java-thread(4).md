---
layout: post
current: post
cover: assets/built/images/java/cover/cover_java.png
navigation: True
title: 쓰레드-실행제어편 (4) 
date: 2021-08-03 00:14:00
tags: [java]
class: post-template
subclass: 'post'
author: nageom
---
쓰레드의 스케줄링을 위해 기초지식 다지기<br>
쓰레드 프로그래밍이 어려운 이유가 동기화(synchronization)과 스케줄링(scheduling) 때문이다. 
이를 잘하기 위해서는 쓰레드의 상태와 관련 메서드의 공부가 필요하다. 
그래서 공부할 것들을 적어봤다. 

> 쓰레드의 상태 

NEW - 쓰레드가 생성되고 아직 START()가 호출되진 않은 상태<br>
RUNNABLE - 실행 중 OR 실행 가능 상태<br>
BLOCKED - 동기화블럭에 의해 일시정지된 상태<br>
WAITING - 실행가능하지 않은(unrrunnable) 일시정지 상태<br>
TIMED_WAITING - 일시정지시간이 지정된 경우의 상태<br>
TERMINATED - 작업이 종료, 소멸<br>

쓰레드의 상태는  Thread의 getState()를 호출해서 확인할 수 있다. (JDK1.5 이상 부터)<br>

쓰레드의 스케줄링과 관련된 메서드와 쓰레드의 움직임을 나타낸 그림이다. 
![ex_screenshot](../../assets/built/images/java/thread/thread(4)_1.jpg)
이걸보면 쓰레드를 머릿속에 그리기 더 쉬울 것이다.<br>
1) 쓰레드 생성 후, start()를 호출하면 일단 실행대기열에 저장된다. <br>
실행대기열은 큐와 같은 구조로 가장 앞 쓰레드가 먼저 실행된다. <br>
2) 실행대기상태에서 차례로 실행한다. <br>
3) 주어진 실행시간이 다되거나 yield()룰 만나면 다시 실행대기열에 들어간다 (제일 뒷자리)<br>
4) 실행 중에 suspend(), sleep(), wait(), join(), I/O block에 의해 일시정지상태가 될 수 있다.
I/O block은 입출력작업에서 발생하는 지연상태를 말한다. 사용자가 입력을 마치면 다시 실행대기 상태가 된다.<br>
5) 지정된 일시정지시간이 다되거나(time-out), notify(), resume(), interrupt()가 호출되면
일시정지상태를 벗어나 다시 실행대기열에 저장되어 자신의 자례를 기다리게 된다. <br>
6) 실행을 모두 마치거나 stop()이 호출되면 쓰레드는 소멸된다. 


위에 적은 메서드들의 실습을 모두 적으면 좋겠지만 너무 길고 많아서 
간단히 보고 떠올릴 수 있을정도만 적으려한다. (자바 750pg참조)

<h6>sleep(long millis) - 일정시간동안 쓰레드를 멈추게 한다. </h6>
- try - catch문으로 예외처리 필수 (일시정지 상태에서 실행대기 상태가 되기 때문)
~~~ javascript
sleep(long millis) - 일정시간동안 쓰레드를 멈추게 한다. 
ThreadEx th1 = new ThreadEx(); //쓰레드 생성
th1.start();
try {
    th1.sleep(2000);   //이런 참조변수를 이용해서 호출할 수 있다. 
}catch(InterruptedException e) {};
~~~
th1.sleep(2000);   
이 메서드는 특정 쓰레드의 참조변수를 사용해서 그 특정 쓰레드를 멈추는 메서드가 아니다. 
th1.sleep을 호출했어도 실제로 영향을 받는 것은 main메서드를 실행하는 main쓰레드이다. 
sleep()메서드는 static으로 선언되어 있어 참조변수를 이용해서 호출하기 보다는
"Thread.sleep(2000);"과 같이 해야 한다.  

메서드 하나하나 올리기엔 좀 귀..ㅊ...ㅣㅏㄴㅎ아서 틈틈ㅎ ㅣ올리는걸로! (2021-08-04 업데이트) <br>

interrupt() - 쓰레드의 작업을 취소시킨다. <br>
멈추는게 아니고 취소시킨다! 
너무 오래걸리는 다운로드를 취소시킬때 사용한다. 

~~~javascript
Thread th = new Thread();
th.start(0;

th.interrupt(); //쓰레드에 interrupt() 호출
class MyThread extends Thread() {
    public void run() {
        while (!interrupted()) {
        }
    }
})

)
~~~
보면 알 수 있듯이 interrupted()는 interrupted상태를 반환한다. <br>
void interrupt() - 쓰레드의 interrupted상태를 false -> true로 전환 <br>
boolean isInterrupted () -쓰레드의 interrupted상태를 그냥 반환. <br>
static boolean interrupted() - 쓰레드의 interrupted상태를 반환하고, false로 변경 <br>
더 자세한 예시는 책에서 확인 ( 753pg ) - (2021-08-08 업데이트)
<br>

suspend() - sleep()처럼 쓰레드를 멈추기함. resume()을 호출해서 다시 실행대기 상태가 되고
stop() 호출 시 즉시 종료 
일반적인 쓰레드 사용 메서드들이지만 교착상태(deadlock)을 일으키기 쉬워 사용이 권장되지 않는다. ('deprecated'되어있음)
(고로 예시는 안적음)

yield() -  다른 쓰레드에게 양보한다. interrupt()를 적절히 사용하여 효율적인 실행을 가능케한다. 
~~~javascript
class yiledTest {
    public static void main(String args[])  {
        ThreadEx th1 = new ThreadEx("*");
        ThreadEx th1 = new ThreadEx("**");
        ThreadEx th1 = new ThreadEx("***");
        th1.start();
        th2.start();
        th3.start();
        
        try {
            Thread.sleep(2000);
            th1.suspend();
            Thread.sleep(2000);
            th2.suspend();
            Thread.sleep(2000);
            th1.resume();
            Thread.sleep(2000);
            th1.stop();
            th2.stop();
            Thread.sleep(2000);
            th3.stop();
        }catch (InterruptedExveption e){}

    }
    
    }

class ThreadEx implements Runnable {
    boolean suspended = false;
    boolean stopped = false;
    
    Thread th;
    
    ThreadEx (String name) {
        th = new Thread(this, name); //쓰레드 생성
    }
    //뤈뤈 
    public void run()  {}

    
    
    
    
}

~~~






참고문서 - 자바의 정석






 
