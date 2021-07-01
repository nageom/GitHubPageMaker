---
layout: post
current: post
cover: assets/built/images/coding/cover_coding.jpg

navigation: True
title: <프로그래머스> 스택/큐 Level 2 기능개발 (1)
date: 2021-06-25 00:14:00
tags: [coding]
class: post-template
subclass: 'post'
author: nageom
---
* * *
<h6> 프로그래머스 > 스택/큐 </h6>
큐를 사용해서 100을 넘은 데이터들은 순서대로 빼내는 문제였다. 

나는 코드를 굉장히 직관적으로 짰다. <br>
que에 progresses를 담고<br>
que.peek()를 이용해 값을 하나씩 꺼내어 <br>
que.peek() + day x speed 이 100을 넘기는지,<br>
넘을때마다 변수 k 에 +1 해주어 반환할 k를 변경시켜주는식 <br>
and 중간중간 맞는 조건문을 넣어주었다 <br>

**[코딩에 잠깐 난관이 있었다면]**<br>
이 문제는 날짜에 따라 **100을 넘은 기능**들이 연속으로 있다면 k를 계속 올려주면 그만이지만 <br>
연속적일지 아닐지는 100이 넘었다는 조건문 안에서 알 수 없기 때문에 que2.offer(k)를 다른 곳에 넣을 수 밖에 없었다. <br>

반대의 **100을 넘지 않는다는 조건**에서
day를 올려주거나 k=0 으로 맞춰주는데 <br>

이 조건에 대해 <br>
바로 전에 100을 넘다가 온 경우에만 k값을 저장해주는 설계를 했기 때문에 
40에서 41로 온것인지를 어떻게 구분해줄것인가를 한참 생각했다. <br>
쉬웠지만 너무 어렵게 생각한것 같다. <br>

boolean check=false를 두고 <br>
**100이 넘은 경우**에는 check=true, <br>
**넘기지 못한 경우**에는 check=true의 조건문을 주고
해당 될때만 k값을 반환할 que2.offer(k)해주고 k=0으로 다시 시작해준다. <br>

**코드를 살펴보자** <br>

~~~ javascript
import java.util.LinkedList;
import java.util.LinkedList;
import java.util.Queue;
class Solution {
    public static int[] solution(int[] progresses, int[] speeds) {

		 
		  // progresses
	      Queue<Integer> que = new LinkedList<>(); 
	      // return 값이 들어갈 que2 
	      Queue<Integer> que2 = new LinkedList<>(); 

	      
	      int i = 0;
	      int day = 1; 
	      int k = 0; //k는 배포 횟수 
	      for(i = 0; i<progresses.length; i++) {
	         que.offer(progresses[i]);
	      }

	      int count=0;
	      i=0;
	      boolean check = false; // 100이 안됐다. 
	       
	      while(i<progresses.length) {
	                                                //            1일 ,  2일     7일
	         int total = que.peek()+(speeds[i]*day); // total = 93+1*1, 93+1*2  93+1*7 // 30 + 30*7 //55 + 5*7
	          
	         if(total>=100) {   //total 93  //94 //95 //100 //240  //
	        	 k++;   //k=1; k=2; // 배포 값 
	        	 i++;   //i=1 i=2;  // 다음 숫자로 넘김 
	        	 que.poll(); //[30,55] //[55]
	        	 check = true; 
	        	 
	        	 if ( i == speeds.length ) {
	        		 que2.offer(k);	 
	        		 count++;
	        	 }
	            
	         }else {    // total=90
	             
	            if(k!=0 && check == true ) { //배포한 후 더이상 배포할 애가 없을때 
	               que2.offer(k); // [2][0][0] 
	               k=0;
	               count++;
	            }
	            check = false;
	            day++;        // j =1 j =2; 7 
	         }
	     
	      }
	  
	      int[] answer = new int[count];
	    
	       
	      int t=0;
	    
	      while(!que2.isEmpty()) {
	    	  answer[t]= que2.poll();
	    	  t++;
	       }
	       
	      
	      return answer;

	   }
}


~~~






<br><br>
커버사진 출처 프로그래머스 