---
layout: post
current: post
cover: assets/built/images/coding/cover_coding.jpg

navigation: True
title: <프로그래머스> 힙(Heap)  Level 3 이중우선순위큐 (2)
date: 2021-06-28 00:14:00
tags: [coding]
class: post-template
subclass: 'post'
author: nageom
---
* * *
<h6> 프로그래머스 > 힙(Heap) </h6>
<br>
**문제 설명** <br>

![ex_screenshot](../../assets/built/images/coding/heap(2)_1.png)
<br>

어렵지 않게 풀 수 있는 문제였다. 
다만 priority queue 에게 지정 원소를 지울 수 있는 remove를 알고 있었다면 더 빨리 풀었을 것이다. 

최댓값, 최솟값을 큐에서 빼내기위해 오름차순, 내림차순의 우선순위 큐를 두 개 생성하고
삽입 명령어 시에는 두 큐에 삽입해 주었고
최솟값 삭제 명령 시에는 내림차순큐.remove(오름차순큐.poll());
최댓값 삭제 명령 시에는 오림차순큐.remove(내림차순큐.poll()); 로 함께 삭제했다.

operations.length만큼 for문을 돌렸기때문에
for문 마지막에 큐가 비었는지 확인하기 어렵지않았다. 
~~~ javascript
import java.util.*;
class Solution {
    public int[] solution(String[] operations) {
            int[] answer = {0,0};
	        PriorityQueue<Integer> ascPq = new PriorityQueue<Integer>(); //오름차순
	        PriorityQueue<Integer> desPq = new PriorityQueue<Integer>(Collections.reverseOrder()); //내림차순 
	        
	        
	        for (int i=0; i< operations.length; i++) {
	        	String[] order = operations[i].split(" ");
	        	int order1 = Integer.parseInt(order[1]);
	        	
	        	switch (order[0]) {
	        		case "I" : 
	        			ascPq.offer(order1);//16
	        			desPq.offer(order1);//16
	        			break;
	        		case "D": 
	        			if (ascPq.size()==0) {break;}
	        			
	        			if (order1 == 1) {//최댓값 삭제
	        				ascPq.remove(desPq.poll());
	        				break;
	        		
	        			}else {// -1  최솟값 삭제시 
	        				desPq.remove(ascPq.poll());
	        				break;
	        			}
	
	        	}
	        	
	        	
	        	if (i == operations.length-1) {  		
	        		if (!ascPq.isEmpty() ) {
	        			answer[0]= desPq.poll();
	        			answer[1]= ascPq.poll();
	        		}
	        	}

	        }
	        return answer;
    }
}
~~~



<br>
<br>커버사진 출처 프로그래머스 