---
layout: post
current: post
cover: assets/built/images/coding/cover_coding.jpg

navigation: True
title: <프로그래머스> 힙(Heap)  Level 2 더 맵게 (1)
date: 2021-06-27 00:14:00
tags: [coding]
class: post-template
subclass: 'post'
author: nageom
---
* * *
<h6> 프로그래머스 > 힙(Heap) </h6>
<br>
**문제 설명** <br>
매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다. 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.

섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)<br>
Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다.<br>
Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.

**제한 사항**<br>
scoville의 길이는 2 이상 1,000,000 이하입니다.<br>
K는 0 이상 1,000,000,000 이하입니다.<br>
scoville의 원소는 각각 0 이상 1,000,000 이하입니다.<br>
모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.<br>
입출력 예<br>

![ex_screenshot](../../assets/built/images/coding/heap(1).png)
<br>


입출력 예 설명<br>
1. 스코빌 지수가 1인 음식과 2인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.<br>
새로운 음식의 스코빌 지수 = 1 + (2 * 2) = 5<br>
가진 음식의 스코빌 지수 = [5, 3, 9, 10, 12]<br>

2. 스코빌 지수가 3인 음식과 5인 음식을 섞으면 음식의 스코빌 지수가 아래와 같이 됩니다.<br>
새로운 음식의 스코빌 지수 = 3 + (5 * 2) = 13<br>
가진 음식의 스코빌 지수 = [13, 9, 10, 12]<br><br>

모든 음식의 스코빌 지수가 7 이상이 되었고 이때 섞은 횟수는 2회입니다.<br>
<br>

<h6>[LinkedList로 풀어봤습니다...] </h6>
![ex_screenshot](../../assets/built/images/coding/heap(2).png)
코드만 보면 될 것 같은데 
효율성이 엉망진창이였다.
~~~ javascript
import java.util.*;
class Solution {
    public int solution(int[] scoville, int K) {
        int answer = 0;
		LinkedList<Integer> list = new LinkedList<Integer>();
	    
	    for (int i=0; i< scoville.length; i++) {
	        list.add(scoville[i]);	
	    }    
        Collections.sort(list);
        
        int sum = 0;
	        
	    while (list.get(0)<K) {
	        Collections.sort(list);
	        sum = list.get(0) + list.get(1)*2;           
		    list.remove(0);
		    list.remove(0);
		    list.add(sum);			        		
		    Collections.sort(list);    
		    answer++;
	    }
      
	    if (answer==0) {
	        answer =-1;
	    }
	    return answer;

    }
}
~~~
Collections.sort가 효율성을 많이 떨어트린것같아 좀 더 공부해봤다. <br>

**Arrays.sort와 Collections.sort의 시간복잡도에 관한 궁금증**<br>

간단히 요약하자면 
Arrays.sort()는 듀얼피봇 퀵정렬로 랜덤 데이터에 대해서 평균적으로 퀵소트 보다 좋은 성능을 낸다. 
Collections.sort() Tim 정렬이라는 삽입(Insertion) 정렬과 합병(Merge) 정렬을 결합하여 만든 정렬을 사용한다.
https://sabarada.tistory.com/138
왜 둘의 정렬 알고리즘이 다른지는 블로그를 위의 블로그를 참조하는 것이 더 좋을 것이다. 

어찌됐든 
while 반복시마다 C * O(N*log(N)) + a 이라는 시간복잡도에 의해 holy..<br>
테스트를 실패했고 시간복잡도가 O(N*logN) 인 우선순위 큐를 사용했고 결과는 성공적이였다. <br>
언제나 어디서나 효율성을 생각하자<br>




<h6>[Priority Queue로 다시 풀었다.]</h6>

~~~ javascript
import java.util.*;
class Solution {
    public int solution(int[] scoville, int K) {
            PriorityQueue<Integer> que = new PriorityQueue<>();
		    int answer = 0;

			for (int i = 0; i < scoville.length; i++) {
				que.offer(scoville[i]);
			}
			
			//int count=0;			
			while(!que.isEmpty()) {				
				if(que.peek() > K) {
					break;
				}
				if(que.size() == 1) {
					if(que.peek()<K) {
						answer=-1;		
						break;
					}	
				}
				
				//이미 첫번째 수가 K보다 작은 경우이니까
				int tmp = que.poll()+ que.poll()*2;
				que.offer(tmp);
				answer++;
				
				
			}
			return answer;
    }

	 
    
    
}
~~~



<br>
<br>커버사진 출처 프로그래머스 