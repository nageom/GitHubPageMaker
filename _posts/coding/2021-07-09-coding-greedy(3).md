---
layout: post
current: post
cover: assets/built/images/coding/cover_coding.jpg

navigation: True
title: <프로그래머스> 탐욕법 큰 수 만들기
date: 2021-07-09 00:14:00
tags: [coding]
class: post-template
subclass: 'post'
author: nageom
---
* * *
**프로그래머스 > 탐욕법 > 큰 수 만들기**<br>
문제 설명<br>
어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.<br>
예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.

문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

제한 조건
number는 1자리 이상, 1,000,000자리 이하인 숫자입니다.
k는 1 이상 number의 자릿수 미만인 자연수입니다.
![ex_screenshot](../../assets/built/images/coding/greedy(3)_2.jpg.png)






<h6>풀이과정</h6>

모랄까.. 느낌은 알겠는데 도저히 코드가 안나와서 다른 분의 코드를 해석했다. 
![ex_screenshot](../../assets/built/images/coding/greedy(3)_1.jpg)

참고 코드 https://velog.io/@hyeon930/<br>



**알게된것**<br>
int num = number.charAt(j) - '0';<br>
문자열-'0'을 하면 문자열를 정수로 바꿔 받을 수 있다. 

<br>
<br><br>
커버사진 출처 프로그래머스 