---
layout: post
current: post
cover: assets/built/images/coding/cover_coding.jpg

navigation: True
title: <프로그래머스> 정렬  Level 2 가장 큰 수(2)
date: 2021-06-30 00:14:00
tags: [coding]
class: post-template
subclass: 'post'
author: nageom
---
* * *
**프로그래머스 > 정렬 > K번째 수**

문제 설명
0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.

제한 사항
numbers의 길이는 1 이상 100,000 이하입니다.
numbers의 원소는 0 이상 1,000 이하입니다.
정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.<br>
**입출력 예**
![ex_screenshot](../../assets/built/images/coding/sort(2)_1.png)


Comparator를 사용해본 적이 없어서 한참 헤맨 문제였다. 
그걸 모르니 자릿수들을 따로 객체에 담아 비교할까, 모든 경우의 수를 구할까 고민했다.


https://programmers.co.kr/learn/courses/30/lessons/42746/solution_groups?language=java 다른 분들의 코드를 보며 계속 출현하는
compare메서드에 
Comparator,Comparable의 공부 필요성을 느끼고
일단 Comparator와 Comparable 공부 + 블로그 포스팅을 마치고 돌아왔다.<br>
이 후 비교적 쉽게 코드를 새로 짤 수 있었고 기분이 매우 좋다. 

공부하고 싶으시다면 제 블로그 https://nageom.github.io/java-comparator-comparable 을 참고하세요. 

**[코드를 살펴보자]**
~~~ javascript
import java.util.*;
class Solution {
    public String solution(int[] numbers) {
        String answer = "";
        String[] strArr = new String[numbers.length];

        for (int i=0; i< numbers.length; i++) {
            strArr[i]= String.valueOf(numbers[i]);
            
        }
        
        Arrays.sort(strArr, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                return (o2+o1).compareTo(o1+o2);
            }
        });
        
        for(String str: strArr) {
            answer+= str;
        }
        
        if (strArr[0].equals("0")) {answer = "0";}
                return answer;

        
    }
}
~~~




<br><br>
커버사진 출처 프로그래머스 