---
layout: post
current: post
cover: assets/built/images/java/cover/cover_java.png
navigation: True
title: 자바의 애너테이션(annotation) 
date: 2021-07-05 00:14:00
tags: [java]
class: post-template
subclass: 'post'
author: nageom
---
***


간단히 프로그램의 소스코드 안에 다른 프로그램을 위한 정보를 미리 약속된 형식으로 포함시킨 것이 바로 애너테이션이다. 
애너테이션은 주석처럼 프로그래밍 언어에 영향을 미치지 않으면서도 다른 프로그램에게 유용한 정보를 제공할 수 있다는 장점을 갖는다.<br> 
예로, 특정 메서드만 테스트하기 원한다면 '@Test' 애너테이션을 메서드에 붙임으로 테스트 프로그램에게
테스트 할 것을 알리는 역할을 하며, 메서드가 포함된 프로그램 자체에 아무런 영향을 미치지 않는다.<br>

또한 애너테이션은 JDK에서 제공하는 표준 애너테이션, 새로운 애너테이션을 정의할 때 사용하는 메타 애너테이션이 있다. <br>

<h6>1. 표준 애너테이션 </h6>
자바에서 기본적으로 제공하는 애너테이션은 많이 없다. 이 마저도 일단 나는 개발경험이 많지 않아서 @override 외에는 사용한 경험이 없다.
그래서 간단한 설명만 덧붙이려한다. <br>
**@Override**<br>
컴파일러에게 오버라이딩하는 메서드라는 것을 알린다. <br>
**@Deprecated**<br>
앞으로 사용하지 않을 것을 권장하는 대상에 붙인다. 
JDK 버전 상승에 따른 기존의 기능을 개선시키고 기능이 추가되는데,
이 과정에서 기존의 기능을 대체할 것들이 추가되어도, 이미 여러 곳에서 사용되고 있을지 모르는 기존의 것들을 함부로 삭제할 수 없어 나온 애너테이션이다. <br>
예를 들어, java.util.Date클래스의 대부분의 메서드는 @Deprecated가 붙어있는데, 
이 메서드 대신에 jdk1.1부터 추가된 Calendar클래스의 get()을 사용하라는 얘기이다. 기존의 것 대신 새로 추가된 개선된 기능을 사용도록 유도한다. <br>

**@SuppressWarnings**<br>
컴파일러의 특정 경고메시지가 나타나지 않게 해준다. <br>
**@SafeVarargs**<br>
지네릭스 타입의 가변인자에 사용한다.(JDK1.7)<br>
**@FunctionalInterface**<br>
함수형 인터페이스라는 것을 알린다.(JDK1.8)<br>
**@Native**<br>
native메서드에서 참조되는 상수 앞에 붙인다. <br>

<h6>2. 메타 애너테이션 </h6>

메타 애너테이션은 '애너테이션을 위한 애너테이션', 즉 애너테이션에 붙이는
애너테이션으로 애너테이션을 저의할 때 애너테이션의 적용대상(target)이나 유지시간(retention)등을 지정하는데 사용한다.
메타 애너테이션은 'java.lang.annotation'패키지에 포함되어 있음

@Target - 애너테이션이 적용가능한 대상을 지정하는데 사용한다.
@Retention - 애너테이션이 유지되는 기간을 지정하는데 사용한다.
그래서 애너테이션 SuppressWarnings를 정의할때,

~~~javascript
@Target({TYPE, FIELD, METHOD, PARAMETER, CONSTRUCTOR, LOCAL_VARIABLE})
@Retention(RetentionPolicy.SOURCE)
public @interface SuppressWarnings {
    String[] value();
}
~~~
이렇게 사용. 
그 외에
@Documented 
애너테이션에 대한 정보가 javadoc으로 작성한 문서에 포함되도록 한다.
@Inherited
애너테이션이 자손 클래스에 상속되도록 한다. 

@Repeatable
@Native..
등등..
애너테이션은 커스터마이징해서 내가 선언할 수도 있지만 그런경우는 극히 드물다. 그래서 따로 설명안함.. 

**Annotation은 애너테이션이 아니라 일반적인 인터페이스로 정의되어 있다.**
java.lang.annotation.Annotation<br>
모든 애너테이션의 조상은 Annotation이다.
그러나 애너테이션은 상속이 허용되지 않으므로 명시적으로 Annotation을 조상으로 지정할 수 없다.
~~~ javascript
@interface TestInfo extends Annotation { //에러
    int count;
    String testedBy();
}
~~~

~~~javascript
package java.lang.annotation;

public interface Annotation { //Annotation 자신은 인터페이스이다. 
    boolean equals(Object obj);
    int hasCode();
    String toString();
    
    Class<? extends Annotation> annotationType(); //애너테이션의 타입을 반환한다.
}

~~~

모든 애너테이션의 조상인 Annotation  인터페이스가 위와 같이 정이되어 있기 때문에, 
모든 애너테이션 객체에 대해 equals(), hashCode() , toString()과 같은 메서드를 bundle호출하는 것이 가능하다.
~~~ javascript
Class<AnnotationTest> cls = AnnotationTest.class;
Annotation[] annoArr = AnnotationTest.class.getAnnotations();

for (Annotation a : annoArr) {
    System.out.println("toString():" + a.toString());
    System.out.println("hashCode():" + a.hashCode());
    System.out.println("equals():"+a.equals(a));
    System.out.println("annotationType():"+a.annotationType());
}
   
~~~
위의 코드는 AnnotatinTest클래스에 적용된 모든 애너테이션에 대해 toStirng(), hashCode(), equlas()를 호출한다. 



참고문서-자바의 정석



 




 
