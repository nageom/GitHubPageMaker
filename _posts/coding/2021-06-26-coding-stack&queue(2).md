---
layout: post
current: post
cover: assets/built/images/coding/cover_coding.jpg

navigation: True
title: <프로그래머스> 스택/큐 Level 2 프린터 (2)
date: 2021-06-26 00:14:00
tags: [coding]
class: post-template
subclass: 'post'
author: nageom
---
* * *
<h6> 프로그래머스 > 스택/큐 </h6>
중요도에 관한 배열이 주어지고 
프린트 요청이 들어온 문서들을 이 배열에 맞춰 재배열하고 
지정한 문서가 몇번째로 프린트되는지 리턴해줘야하는 <U>QUEUE</U>를 이용한 '프린터'문제이다. 

<h6>[무슨 생각으로 두시간을 보냈는가]</h6>
일단 두시간 넘게 못풀었다. 
처음 해결방법으로는 location의 인덱스를 같이 저장할 방법으로
큐 안에 map을 넣을 수는 없을까는데 당연히 안됐고
두번째로 큐의 정렬에 따라서 배열을 재정렬 시켜주는 방법이였는데 ㅎ 그것도 못했다. 

도저히 안되서 풀이를 보고나니 허탈해졌다. 맵 대신 객체를 넣으면 되는것을.. 후..
문제풀이 경험이 많이 부족하다는 것을 한번 더 깨달았다. 

거두절미하고 코드를 살펴보자
~~~ javascript

import java.util.*;
class Solution {
    public int solution(int[] priorities, int location) {
    
        //queue를 사용하는데, que안에 기본자료형이 아닌 객체를 생성해서 담아줌으로써 location위치도 같이 움직이도록한다. 
		int answer = 0;
	        class Prior {
	            int index;
	            int value; 
	            
	            Prior (int i, int v) {
	                index = i;
	                value = v;
	                
	            }
	        }
	        
	        Queue<Prior> que = new LinkedList<Prior> ();
      
	        for (int i=0; i< priorities.length; i++) {
	        	que.offer(new Prior(i, priorities[i]));	
	        }
	        
	        
	       // int count =0; 
	        while (!que.isEmpty()) {
	            boolean check = false;
	            
	            int first = que.peek().value;
	            
	            for (Prior tmp : que) {                
	                if (first < tmp.value ) {
	                    check = true;
	                    break;
	                }
	                
	                
	            }
	            
	            if(check) {
	            	que.offer(que.poll());
	                              
	            }else {
	                if (que.poll().index == location ) {
	                	//6 - 4 
	                    answer = priorities.length - que.size();              
	                }
	                
	            }

	        }//while 끝
			return answer;
	   
	    }
}




~~~



<br><br>
References
https://velog.io/@qweadzs/%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EC%8A%A4-%ED%94%84%EB%A6%B0%ED%84%B0-java
<br>커버사진 출처 프로그래머스 