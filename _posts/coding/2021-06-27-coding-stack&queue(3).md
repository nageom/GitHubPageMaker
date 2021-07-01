---
layout: post
current: post
cover: assets/built/images/coding/cover_coding.jpg

navigation: True
title: <프로그래머스> 스택/큐  Level 2 주식가격 (3)
date: 2021-06-27 00:14:00
tags: [coding]
class: post-template
subclass: 'post'
author: nageom
---
* * *
<h6> 프로그래머스 > 스택/큐 </h6>

문제 설명<br>
초 단위로 기록된 주식가격이 담긴 배열 prices가 매개변수로 주어질 때, 가격이 떨어지지 않은 기간은 몇 초인지를 return 하도록 solution 함수를 완성하세요.<br>

제한사항<br>
prices의 각 가격은 1 이상 10,000 이하인 자연수입니다.<br>
prices의 길이는 2 이상 100,000 이하입니다.<br><br>
입출력 예<br>
prices &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 	return<br>
[1, 2, 3, 2, 3]	[4, 3, 1, 1, 0]<br><br>
입출력 예 설명<br>
1초 시점의 ₩1은 끝까지 가격이 떨어지지 않았습니다.<br>
2초 시점의 ₩2은 끝까지 가격이 떨어지지 않았습니다.<br>
3초 시점의 ₩3은 1초뒤에 가격이 떨어집니다. 따라서 1초간 가격이 떨어지지 않은 것으로 봅니다.<br>
4초 시점의 ₩2은 1초간 가격이 떨어지지 않았습니다.<br>
5초 시점의 ₩3은 0초간 가격이 떨어지지 않았습니다.<br>

<h6> 느낀점 </h6>
쉬운 문제였다. 
큐를 사용했고 친구는 사용하지 않고도 풀 수 있다고 했다. 


<br>
<h6>[코드를 살펴보자]</h6>

~~~ javascript
    import java.util.*;
    class Solution {
    public int[] solution(int[] prices) {
        Queue<Integer> que = new LinkedList<Integer> ();
        Queue<Integer> que2 = new LinkedList<Integer> ();
        
        for(int i=0; i< prices.length; i++) {
            que.offer(prices[i]);
        
        }
        int size = que.size(); 
        for (int i=0; i< size; i++)  {
        	int count = 0; 
        	
        	int first = que.poll();
        	
        	for (int tmp : que) {  		
        		//작거나 같으면 떨어지지않음
        		// 3 <= 2 
        		if (first <= tmp) {
        			count++;        			
        		}else {
        			count++;
        			break;
        		}  	
        	}

        	que2.offer(count);
   	
        }
        

        int[] answer = new int[que2.size()];
       
        for (int i=0; i<answer.length; i++) {
        	
        	answer[i]= que2.poll();
        	
        }
        
        
        return answer;
    }
}
~~~



<br>
<br>커버사진 출처 프로그래머스 