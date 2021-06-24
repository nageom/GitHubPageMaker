---
layout: post
current: post
cover: assets/built/images/java/cover/cover_equals.jpg
navigation: True
title: a
date: 2021-06-23 00:14:00
tags: [java]
class: post-template
subclass: 'post'
author: nageom
---
***
## 배열<br>

- 선언 : int[] a = new int[8];<br>
  int[] a = {1,2,3,4,5};<br>
- 배열 -> 문자열 : Arrays.toString();<br>
- char 배열 -> 문자열 : String.valueOf(); <br>
- 문자열 -> char : .toCharArray;<br><br>

- 배열 오름차순 : Arrays.sort(arr);<br>
- 배열 내림차순 : Arrays.sort(arr, Collections.reverseOrder());<br><br>

- 배열의 길이 : arr.length;<br>
- 2차원 배열의 길이 : arr[0].length; 0번째 배열의 길이<br><br>

- 배열의 특정 범위만 빼기 : Arrays.copyOfRange(arr, 2 ,4 ); 2번째 인자(포함)부터 3번째 인자(미포함) 앞까지 추출)<br>
  <br>

## 문자열<br>
<br>
- 선언 : String str = "";<br><br>

- str.startWith(a); : 특정 문자로 시작하는지 판단<br>
- str.endWith(a); : 특정 문자로 끝나는지 판단<br>
  <br>
- str.equals(a); : 같은지 아닌지 판단<br>
- str.indexOf("a"); : a가 몇번째 위치하는지 판단<br>
  <br>
- str.length; : 문자열길이판단<br>
- String[] strArr = str.split("") : 문자열 1개씩 나누어 배열로 반환, 넣는 값을 기준으로 나눌수도있음 (str.split(" ")<br>
- str.substring(0, 2); : 1번째 인자부터 2번째 인자 앞까지 문자추출<br>
- str.toLowerCase : 모든문자 소문자 변환<br>
- str.toUpperCase : 모든문자 대문자 변환<br>
  <br>
- str.trim(); : 문자열 빈칸 제거<br>
- String.valueOf(int i) : i를 문자열로 변환<br>
  <br>
- str.charAt(i) : i번째 문자 추출<br>
  <br>
- StringBuilder sb -> sb.toString : StringBuilder을 문자열로 변환<br>
- sb.append(); : 문자열 뒤에 붙임 <br>
  <br>

# 우선순위 큐 생성 
~~~javascript
PriorityQueue<String> pq = new PriorityQueue<>();
    pq.offer("b");
    pq.offer("a");
    pq.offer("c");
    pq.offer("d");
    pq.offer("f");

while(!pq.isEmpty()) {
     System.out.println(pq.poll());
}
~~~
# StringBuilder 
~~~ javascript
	StringBuilder sb = new StringBuilder(); 
		sb.append("abc");
		sb.append("ghi");
		sb.append("def");
		//sb.reverse();거꾸로
		
		System.out.println(sb);
		

~~~
# 깊은 복사
~~~ javascript
ArrayList<Integer> w=new ArrayList<Integer>();
		ArrayList<Integer> copy_w=new ArrayList<Integer>();
		copy_w.addAll(w);

~~~


# set -> list 
~~~ javascript
ListPermalink
set => List 변경Permalink
생성자에 값을 넣어주면, set -> List로 변경할 수 있다.
Set<String> set = new HashSet<String>();
List<String> menuList = new ArrayList<>(set);
~~~
