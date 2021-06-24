---
layout: post
current: post
cover: assets/built/images/algorithm/cover.png

navigation: True
title: <정렬> 삽입 정렬(Insertion Sort)
date: 2021-06-22 00:14:00
tags: [algorithm]
class: post-template
subclass: 'post'
author: nageom
---
* * *
> <h3> 삽입 정렬(Insertion Sort) </h3>
<h6>[각 숫자를 적절한 위치에 삽입하는 방법 ]</h6>
필요할 때만 위치를 바꾸기 떄문에 <br>
버블 정렬, 선택정렬보다 더 빠르다. (O(N^2) 중에서)<br>
그렇지만 정렬이 되어있지 않은 경우는 다름없는 O(N^2) 이기때문에 항상 비효율적이지 않다고는 말할 수 없다. <br><br>

int arr[10]= {1,10,5,8,7,6,4,3,2,9}<br>
처음부터 하나씩 앞의 배열값들과 비교하며 선택값을 본인보다 작은값을 만났을때 작은값 <br>
바로 뒤에 삽입해준다.<br>
버블 정렬과 뭐가 다른가 할 수 있는데, <br>
삽입 정렬은 앞의 원소들이 이미 정렬이 되어있다 가정하기 때문에 <br>
작은값을 만났을때에만 조심스럽게 비교연산을 시작해서 속도가 줄어들 수 밖에 없다. <br><br>
1 5 10 8 7 6 4 3 2 9<br>
1 5 8 10 7 6 4 3 2 9<br>
1 5 7 8 10 6 4 3 2 <br>

<h6>공부하다 드는 생각</h6>
그럼 말 그대로 삽입정렬이라 삽입을 하게 되면 그 자리에있던 데이터들이 한 칸씩 자리 이동을 해주어야한다.
그럼 삽입이 아니고 변경인가라고 생각했는데  <br><br>
코드를 보니 느낌은 삽입이고 자리의 변경이 맞았다. <br>
if (array[i] > array[i+1]) 이 경우에만 자리를 바꿔준다.  <br>
무조건 비교하는 정렬법이 아니라 이미 앞 원소들은 정렬이 된 상태이기 때문에 비교할 필요가 없는것이 장점이다.  <br>
이러한 특징으로 특정한 상황에서 속도가 굉장히 빠를 수 있다. <br>
<br>


<h6>코드를 살펴보자</h6>
~~~ javascript
# include <stdio.h>

int main(void) {
	
	//삽입 정렬을 만들어 보자
	int arr[10]= {1,10,5,8,7,6,4,3,2,9};
	int arrSize = sizeof(arr)/sizeof(int);
	int tmp, j=0;
	
	
	for (int i=1; i<arrSize; i++) {
			j = i; 
		while (arr[j]<arr[j-1]) {// 앞의 값이 나보다 클때에만 while문 
			tmp = arr[j];
			arr[j]= arr[j-1];
			arr[j-1]= tmp;
			j--;		
	 }

	}
	for (int i=0; i<arrSize; i++) {
		printf("%d ", arr[i]);
	
	}

}
~~~
<h6>[버블 정렬의 시간 복잡도 O(N^2) ]</h6>

정렬이 거의 되어있지 않은 상황에는 <br>
10+8+7+...+1 으로 O(N*N) 의 시간복잡도에 충실하게 되지만 <br>

<h6>'거의 정렬된 상태'</h6> 
라면 정렬이 거의 되어있는 <br>
arr={2,3,4,5,6,7,8,9,10,1}<br>
<br>
'1'을 빼고는 거의 한번씩의 연산만 지나치게되어 아주 빠른 정렬 속도 
즉, 퀵 정렬 보다 더 빠르거나 동등한 속도를 낼 수 있다. <br>


References <br>
https://www.youtube.com/watch?v=16I9Z7bS1iM&list=PLRx0vPvlEmdDHxCvAQS1_6XV4deOwfVrz&index=5


