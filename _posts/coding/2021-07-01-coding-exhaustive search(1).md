---
layout: post
current: post
cover: assets/built/images/coding/cover_coding.jpg

navigation: True
title: <프로그래머스> 완전탐색  Level 1 모의고사(1)
date: 2021-07-01 00:14:00
tags: [coding]
class: post-template
subclass: 'post'
author: nageom
---
* * *
**프로그래머스 > 완전탐색 > 모의고사**

문제 설명<br>
수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.

1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...<br>
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...<br>
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...<br>

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.
<br>
제한 조건<br>
시험은 최대 10,000 문제로 구성되어있습니다.<br>
문제의 정답은 1, 2, 3, 4, 5중 하나입니다.<br>
가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.<br>
**입출력 예**<br>
![ex_screenshot](../../assets/built/images/coding/exhaustive search(1)_1.png){: width="600" height="100}{: .center}

입출력 예 설명
입출력 예 #1<br>
수포자 1은 모든 문제를 맞혔습니다.<br>
수포자 2는 모든 문제를 틀렸습니다.<br>
수포자 3은 모든 문제를 틀렸습니다.<br>
따라서 가장 문제를 많이 맞힌 사람은 수포자 1입니다.<br>

입출력 예 #2

모든 사람이 2문제씩을 맞췄습니다.

<h6>[풀이과정]</h6>
   
우선 수포자들이 갖는 배열이 제시되는 수학문제답 배열의 크기와 같지 않음으로
수학문제답 배열 크기만큼 계속 반복되도록 i % (수포자답 배열 길이) 를 사용했다.<br>
1번 수포자 = {1,2,3,4,5} 를 예로 들면 <br>
0%5 = 0<br>
1%5 = 1<br>
2%5 = 2<br>
.<br>
.<br>
5%5 = 0<br>
6%5 = 1<br>
나머지 값은 길이를 5로 갖는 배열의 인덱스 값이 나온다. <br>

다음으로 return 되는 값은 가장 많이 문제를 맞힌 사람이 들어간다. 
동점이 있을경우 같이 return 된다. 

나는 순서를 매겨서 return 해줘야 하는줄 알고 새로 객체를 생성할까 라는 생각까지했다.
다른 사람들은 이런 실수 안하겠지! 


**[코드를 살펴보자]**
~~~ javascript
public int[] solution(int[] answers) {
        int[] p1 = {1,2,3,4,5};
		int[] p2 = {2,1,2,3,2,4,2,5};
		int[] p3 = {3,3,1,1,2,2,4,4,5,5};
        
        Queue<Integer> que = new LinkedList<Integer>();

        
        int res1=0;
        int res2=0;
        int res3=0;
        
        for(int i=0; i<answers.length; i++) {
            if(p1[i%p1.length]==answers[i]) {res1++;}
            if(p2[i%p2.length]==answers[i]) {res2++;}
            if(p3[i%p3.length]==answers[i]) {res3++;}     
        }
        int max = Math.max(Math.max(res1, res2), res3);
        if(max == res1) {que.add(1);}
        if(max == res2) {que.add(2);}
        if(max == res3) {que.add(3);}
        
        
        int[] answer = new int[que.size()];
        
        
        for(int i=0; i< answer.length; i++) {

            answer[i] = que.poll();
        }


            
        return answer;
    }
~~~
**코드 설명**<br>
Math.max(a,b)는 두개의 인자값을 비교하여 더 큰 값을 return 한다. <br>
반대로 Math.min도 존재한다. <br>

answer 배열의 크기를 모르는 상태에서 값을 넣어줘야함으로 queue를 사용했다. 



<br><br>
커버사진 출처 프로그래머스 