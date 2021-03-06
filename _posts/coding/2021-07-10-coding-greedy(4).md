---
layout: post
current: post
cover: assets/built/images/coding/cover_coding.jpg

navigation: True
title: <프로그래머스> 탐욕법 구명보트
date: 2021-07-10 00:14:00
tags: [coding]
class: post-template
subclass: 'post'
author: nageom
---
* * *
**프로그래머스 > 탐욕법 > 구명보트**<br>
문제 설명<br>
무인도에 갇힌 사람들을 구명보트를 이용하여 구출하려고 합니다. 구명보트는 작아서 한 번에 최대 2명씩 밖에 탈 수 없고, 무게 제한도 있습니다.<br>
예를 들어, 사람들의 몸무게가 [70kg, 50kg, 80kg, 50kg]이고 구명보트의 무게 제한이 100kg이라면 2번째 사람과 4번째 사람은 같이 탈 수 있지만 1번째 사람과 3번째 사람의 무게의 합은 150kg이므로 구명보트의 무게 제한을 초과하여 같이 탈 수 없습니다.

구명보트를 최대한 적게 사용하여 모든 사람을 구출하려고 합니다.

사람들의 몸무게를 담은 배열 people과 구명보트의 무게 제한 limit가 매개변수로 주어질 때, 모든 사람을 구출하기 위해 필요한 구명보트 개수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

제한사항
무인도에 갇힌 사람은 1명 이상 50,000명 이하입니다.
각 사람의 몸무게는 40kg 이상 240kg 이하입니다.
구명보트의 무게 제한은 40kg 이상 240kg 이하입니다.
구명보트의 무게 제한은 항상 사람들의 몸무게 중 최댓값보다 크게 주어지므로 사람들을 구출할 수 없는 경우는 없습니다.

![ex_screenshot](../../assets/built/images/coding/greedy(4)_1.jpg.png)

<h6>풀이과정</h6>
해도해도 안풀려서 질문하기를 봤는데, 
문제 설명에 '구명보트는 작아서 한 번에 최대 2명씩 밖에 탈 수 없고'를 무시한 사람들이 있었다.
그리고 그게 나였다. 이 조건을 무시하니 테스트케이스에서 막혔다.  
![ex_screenshot](../../assets/built/images/coding/greedy(4)_3.jpg.png)
![ex_screenshot](../../assets/built/images/coding/greedy(4)_2.jpg.png)

이후에 다시 코드를 짜는데 
배열을 둘 씩 묶어서 연산을 해볼까 했는데, 그렇게되면 제약이 너무너무 많아서 패스하고
정렬된 배열의 가장 작은 값과 큰값으로 연산을 사용하니 쉽게 풀 수 있었다. 
어렵지 않아서 코드를 보면 이해가 될거다. 

~~~javascript
package greedy;
import java.util.*;
public class LifeBoat {

	 public static int solution(int[] people, int limit) {
	        int answer = 0;
	        
	        Arrays.sort(people);//50 50 70 80
	       
	        int start = 0;
	        for (int end = people.length-1 ; end>=start; end--) {
	        	if(people[start]+ people[end] > limit) {
	        		answer++;
	        	}
	        	else {
	        		start++;
	        		answer++;
	        	}
	        	
	        }
	       
	        
	        return answer;
	    }
	
	
	public static void main(String[] args) {
		int[] people = {70, 80, 50};
		int[] people2 = {70, 50, 80, 50};
		int[] people3 = {40,40,80};

		int limit = 100;
	
		System.out.println(solution(people3, limit));
		
	}
	
	
	
}

~~~



<br>
<br><br>
커버사진 출처 프로그래머스 