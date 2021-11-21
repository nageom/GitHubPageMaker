---
layout: post
current: post
cover: assets/built/images/java/cover/cover_java.png
navigation: True
title: 추상과 인터페이스 
date: 2021-06-17 00:14:00
tags: [java]
class: post-template
subclass: 'post'
author: nageom
---
***
면접질문 공부하는데 추상클래스와 인터페이스 차이가 헷갈려서 해보는 포스팅이다 <br>
그래서 이번에 구입한 자바의정석으로 공부하고 포스팅 도전 <br>

<h6> 추상클래스 </h6>
<br>
추상클래스는 미완성 설계도라고 보면됩니다. 
좀 더 자세히 보자면 클래스의 미완성이 멤버의 개수에 관계된 것이 아니라, 단지 미완성 메서드(추상메서드)를 포함하고 있다는 의미입니다.<br>
특징이라하면 아무래도 미완성 설계도로는 완성된 제품을 만들 수 없듯이 추상클래스로 인스턴스를 생성할 수는 없습니다.<br>

저는 추상클래스를 볼때 추상클래스는 "도형" -> 딱 정해진 형태가 없는 추상적인 형체 
상속받은 클래스는 "원형", "사각형", "삼각형" -> 구현된 형체 를 예로 듭니다. 
이 셋 모두 도형이라는 큰 틀에 들어맞죠. 

즉, 추상클래스는 상속을 통해 오직 자손클래스에 의해서만 완성될 수 있습니다. 
두번째로는 추상클래스를 상속받은 클래스가 미완성 메서드를 반드시 재정의 해줘야합니다.

<h6> 추상메서드(abstract method)</h6>
메서드는 선언부와 구현부(몸통)으로 구성되어 있는데<br>
추상메서드는 선언부만 작성하고 구현부는 작성하지 않은 채로 남겨둡니다
<br><br>
<h6>사용이유?</h6><br>
여러 객체를 부모클래스로 하나의 list에 모으기 편리함 때문 <br>
재정의를 강조하기 위해

추상클래스는 키워드 'abstract'를 붙이기만 하면 됩니다. <br>
~~~javascript
abstract class 추상클래스 이름 {
    abstract void play(int pos);
    abstract void stop();
}
//상속 받을때는 확장이라는 뜻의 extends 사용
class 자식클래스 extends 추상클래스 {
    void play(int pos) {/*생략*/}
    void stop() {/*생략*/}
}
~~~
<h5> 인터페이스 </h5>
일종의 추상클래스<br>
인터페이스는 추상클래스처럼 추상메서드를 갖지만 추상클래스보다 <br>
추상화 정도가 높아서 추상클래스와 달리 몸통을 갖춘 일반 메서드 또는 멤버변수를 구성원으로 가질 수 없다.
<br>
class에서 상속시에 interface를 사용한다. 

<h6>인터페이스 특징 </h6>
특징 1. 제약사항 <br>
- 모든 멤버변수는 public static final 이어야하고, 생략가능
- 모든 메서드는 public abstract 이어야 하며, 생략 가능
단, static 메서드와 디폴트 메서드는 예외(jdk1.8부터)
  
~~~javascript
interface Car {
    public static final int wheel=4;
    final int handle=1;
    static int door=4;
    int window = 6;
    
    public abstract void drive();
    void stop();// public abstract void stop();
}
~~~
특징2. 인터페이스는 인터페이스로부터만 상속 받을 수 있으며, 클래스와는 달리 다중상속, 즉 여러 개의 인터페이스로부터 상속을 받는 것이 가능하다. 
<br>
~~~javascript


interface A { void move(int x, int u);}
interface B { void stop(int d);}

interface D extends A, B {

}

public class One implements D{


    @Override
    public void move(int x, int u) {
    // TODO Auto-generated method stub

}

    @Override
    public void stop(int d) {
        // TODO Auto-generated method stub

    }


}

~~~
인터페이스 D에 정의된 멤버가 하나도 없지만 조상 인터페이스로부터 상속받은 
두개의 추상메서드 move(int x, int y)와 attack(D d)을 멤버로 갖게 된다.<br>

특징.3 <br>
추상클래스처럼 그 자체로는 인스턴스를 생성할 수 없으며,<br>
추상클래스는 확장한다는 의미의 키워드 'extends'를 사용하지만 <br>
-> 일반 클래스와 추상 클래스 상속엔 'extends'<br>
-> interface가 interface 상속에도 'extends'<br>

인터페이스는 구현한다는 의미의 키워드 'implements'를 사용한다.<br>
-> 일반 클래스가 interface 상속때에 'implements' <br>


<H6> 추상 클래스와 인터페이스 차이점</H6>
추상 클래스는 <br>
 -관련성이 높은 클래스들 간에 코드를 공유하고 싶은 경우<BR>
 공통점을 모아 만든 클래스.<BR>
 -추상 클래스를 상속 받을 클래스들이 공통으로 갖는 메소드와 필드가 많은 경우<br> 

인터페이스 <br>
 - 서로 관련성이 없는 클래스들의 인터페이스를 구현하게 되는 경우 <br>
 - 특정 기능을 넣고 싶은데 어디서 어떻게 행동이 구현되는지는 신경쓰지 않는 경우 <br>
 - 다중상속을 허용하고 싶은 경우 <br>







 
