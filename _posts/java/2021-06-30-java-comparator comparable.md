---
layout: post
current: post
cover: assets/built/images/java/cover/cover_java.png
navigation: True
title: Comparator와 Comparable
date: 2021-06-30 00:14:00
tags: [java]
class: post-template
subclass: 'post'
author: nageom
---
> 자주 쓰이는 Arrays.sort() 를 이용해 배열을 정렬할 때, 사실 내림&오름차순 말고도 원하는 대로
> 정렬이 가능한데 이를 가능하게 해주는 인터페이스 두가지를 소개하고자한다. <br>

<h6> Comparator와 Comparable </h6>
자주 쓰이는 Arrays.sort()를 호출만 하면 컴퓨터가 알아서 배열을 정렬하는 것처럼 보이지만, 사실은 
Character클래스의 Comparable의 구현에 의해 정렬되었던 것이다. 
Comparator와 Comparable은 모두 인터페이스로 컬렉션을 정렬하는데 필요한 메서드를 정의하고 있으며
Comparable을 구현하고 있는 클래스들은 같은 타입의 인스턴스끼리 서로 비교할 수 있는 클래스들, 주로 Integer 와 같은
wrapper클래스와 String, Date, File과 같은 것들이며 기본적으로 오름차순으로 구현되어 있다. 
그래서 <U>Comparable을 구현한 클래스는 정렬이 가능하다는 것을 의미한다. </U> 


Comparator와 Comparable의 실제 소스
~~~javascript
public interface Comparator{
    int compare(Object o1, Object o2) {
        boolean equals(Object obj);
    }
}
public interface Comparable {
    public int compareTo(Object o);
}

~~~
참고 : Comparable은 java.lang패키지에 있고, Comparator는 java.util패키지에 있다. 

compare()와 compareTo()는 선언형태와 이름이 약간 다를 뿐 두 객체를 비교한다는 같은 기능을 목적으로한다. 
compareTo()의 반환값은 int로 비교하는 두 객체가 같으면 0, 비교하는 값보다 작으면 음수, 크면 양수를 반환하도록 구현해야한다.<br> 
compare()도 이와 동일.<br>

**Integer클래스의 compareTo메서드**
~~~javascript
public final class Integer extends Number implements Comparable {
    public int compareTo(Integer anotherInteger) {
        int thisVal = this.value;
        int anotherVal = anotherInteger.value;

        //비교하는 값이 크면 -1, 같으면 0, 작으면 1을 반환한다. 
        return (thisVal<anotherVal ? -1  : (thisVal == anotherVal ? 0 : 1 ));
    }


}
~~~


그냥 보자면 목적도 같고 생김새도 같은 둘이라서 공통점만 알겠는데? 싶지만 <br>
자세히 보면 둘의 차이는 <U>매개변수, 비교 대상</U>에 있다. <br>
Comparable은 자기 자식과 매개변수 객체를 비교하는 인터페이스이고, <br>
Comparator는 두 매개변수 객체를 비교하는 인터페이스이다. <br>
즉, 본질적으로 비교한다는 것 자체는 같지만, 비교 대상이 다르다는 것이다.<br>






또한, 
위와 같이 익명 객체(클래스)를 이용해서 comparator의 기능만을 사용할 수 있다. 

~~~javascript
public static void main(String[] args) {

    // 문자 길이로 sorting (오름차순)
    Arrays.sort(arr, new Comparator<String>() {
    @Override
        public int compare(String s1, String s2) {
            return s1.length() - s2.length();
        }
    });
	}
	
~~~

![ex_screenshot](../../assets/built/images/java/basic of java/comparator(1).png)


그래서 Arrays의 메서드 sort를 이용한 정렬을 사용시 원하는 정렬이 있다면 익명 클래스를 이용한 Comparator를 구현하는 경우가 많다.<br>
static void sort(Object[] a) //는 객체 배열에 저장된 객체가 구현한 Comparable에 의한 정렬<br>
static void sort(Object[] a , Comparator c) //지정한 Comparator에 의한 정렬이라 보면 된다. <br>

다만 compare()의 매개변수가 Object 타입이기 때문에 compareTo()를 바로 호출할 수 없으므로 먼저 Comparable로 형변환해야 한다는 것을 명심하자.
매개변수를 Integer, String 등으로 받는 경우에 형변환 필요없이 바로 compareTo()를 호출이 가능하다.

참고문서 - 자바의 정석 






 
