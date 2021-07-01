---
layout: post
current: post
cover: assets/built/images/algorithm/cover.png

navigation: True
title: <정렬> 퀵 정렬 (Quick Sort)
date: 2021-06-24 00:14:00
tags: [algorithm]
class: post-template
subclass: 'post'
author: nageom
---
* * *
<h6>퀵 정렬 알고리즘</h6>
시간 복잡도 O(N^2)를 갖는 알고리즘은 10만 개가 넘어가면 일반적인 상황에서 사용하기가 매우 어렵다. 정말 오래걸린다는 말이다. <br>
그리하여 나온 빠른 정렬 알고리즘이 퀵 정렬 알고리즘이다. <br>
'분할 정복' 알고리즘으로 평균 속도가 O(N* log2N) 이다. <br>
이름 그대로 정말 빠른 정렬 <br>

log2N이라면 얼마인가보면 <br>
2 ^ 10 = 1,000 이고 <br>
2 ^ 20 = 1,000,000 인데 <br>
log2N -> N이 1,000,000일 때는 ? 20이다. <br>
고로 엄청 빠르다. <br>

<h6>[특정한 값을 기준으로 큰 숫자와 작은 숫자를 나누자]</h6>

읽기 전에 머리 터짐을 방지하기 위해 간단히 생각 적어둘 규칙
1) 왼쪽끝에서 나보다 큰 값 찾으러 오른쪽으로 이동
2) 오른쪽끝에서 나보다 작은 값 찾으러 왼쪽으로 이동

3) 엇갈리면 내 위치 바꿈
4) 바뀐 자리 중심으로 분할 


<br>
int[] arr = {3 7 8 1 5 9 6 10 2 4};
<U>3</U> 7 8 1 5 9 6 10 2 4 (3 밑줄)
피봇 값을 기준으로 왼쪽끝에서 오른쪽으로 피봇값보다 큰 값을 찾고, <br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 오른끝에서 왼쪽으로 피봇값보다 작은 값을 찾아<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 서로 바꿔준다. <br>
<U>3</U> 2 8 1 5 9 6 10 7 4  (2와 7 위치 바꿈) (3 밑줄)

<U>3</U> 2 1 8 5 9 6 10 7 4  (3 밑줄)
계속 나아가다가 결국 값들끼리 위치가 엇갈리게 됐을 때<br>
즉, 작은값의 인덱스가 큰 값의 인덱스보다 더 작을 때<br>
왼쪽에 있는 값 (작은값)과 피봇 값을 바꿔준다. <br>
<U>1</U> 2 **3** <U>8</U> 5 9 6 10 7 4 <br>

피봇 값의 위치가 바뀐 뒤에는 바뀐 위치를 기준으로 <br>
왼쪽의 값들은 피봇값보다 작고<br>
오른쪽의 값들은 피봇값보다 크다는 특징을 갖는다. (두 집합으로 분할됨)<br>

피봇값의 위치가 바뀐 뒤 바뀐 위치를 기준으로 왼쪽 데이터들, 오른쪽 데이터들 두 집합으로 분할되었다. <br>
두 개의 배열이 되었다고 생각하면 더 편하다<br>
나누었으니 이제 피봇값은 두개가 되고, <br>
각각 처음처럼 비교를 시작한다.<br>
           
<U>1</U> 2 **3** <U>8</U> 5 9 6 10 7 4 <br>

'1' 피봇값을 기준으로 비교를 해봤지만 결국 '1'에서 다시 만났다.<br>
이런 경우도 엇갈렸다고 인식하고 1과 '1' 자기자신을 바꾼다. <br>

그래서 다시 정렬이 된다.<br>

**1** <U>2</U> **3** <U>8</U> 5 9 6 10 7 4 <br>

위에서도 말했다시피 <br>
엇갈리면 어쩐다? 위치 바꾸고 바뀐 위치를 기준으로 왼쪽 데이터들, 오른쪽 데이터들 두 집합으로 분할하여<br>
또 비교연산한다.<br>
이번엔 2가 피봇값인데 위와같이 그자리를 지키게 된다.<br>


**1 2 3** <U>8</U> 5 9 6 10 7 4 <br>


**1 2 3** <U>8</U> 5 4 6 10 7 9 <br>


**1 2 3** <U>8</U> 5 4 6 7 10 9<br>

엇갈림. 피봇보다 작은 값과 피봇값 위치 바꿔줌. 새로 분할<br>
                 
**1 2 3** <U>7</U> 5 4 6 **8** <U>10</U> 9 <br>

이렇게 반복 <br>
1 2 3 4 5 6 7 8 9 10 완성 <br>

<h6>[코드를 살펴보자]</h6>
~~~ javascript
#include <stdio.h>

int number = 10;
int data[10] = {1,10,5,8,7,6,4,3,2,9};

//start 정렬을 수행하는 부분집합의 첫 원소 
//end 정렬을 수행하는 부분집합의 마지막 원 
void quickSort(int *data, int start, int end) {
	
	if (start >= end) { // 원소가 1개인 경우
		return ;  
	}

	int key = start; //키는 첫번째 원소
	// 피봇 값과 비교할 바로 오른쪽 값들 
	// 즉, 왼쪽 -> 오른쪽 비교의 출발지점  
	int i =  start + 1;
	
	// 피봇 값과 비교할 오른쪽 끝의 값들 
	//즉, 오른쪽 -> 왼쪽 비교의 출발지점 
	int j = end; 
	int temp; // 값 이동을 위한 변수 
	
	while ( i <= j ) {// 엇갈리지 않을때 까지만  반복 (엇갈리면 i> j) 
		while(data[i] <= data[key]) { //피봇값보다 큰 값을 찾으러 간다.  
		 	i++;
		 	
		}
		 while(data[j] >= data[key] && j > start)  { //피봇값보다 작은 값이 나올때까지 반복
		 										    // && 값이 넘어가지않게 결어줌  
		 	j--;
		 	
		}
		if(i > j) {	//현재 엇갈린 상태면 키 값과 교체 
			temp = data[j];
			data[j] = data[key];
			data[key]= temp;		
		}else {
			temp = data[j];
			data[j] = data[i];
			data[i] = temp;
		}
	
	} 
	//엇갈려서 피봇값의 위치가 바뀌고 
	//분열이 된 후 
	//start, end를 새로 지정해 퀵정렬해간다.  
	quickSort(data, start , j-1);
	quickSort(data, j+1, end); 
	 
}
int main(void) {
	quickSort(data, 0, number-1);
	for (int i=0; i< number; i++) {
		printf("%d ", data[i]);
		
		
	}
	
	
}

~~~
<h6>[퀵 정렬의 시간 복잡도 O(N* log2N) ]</h6>
<br>
삽입,버블,선택 정렬의 시간 복잡도로는<br>
1 2 3 4 5 6 7 8 9 10 에 대해<br>
N^2 = 10 * 10 = 100<br>

퀵 정렬의 시간 복잡도로는 <br>
1 2 3 4 5 => 5 * 5 = 25<br>
6 7 8 9 10 => 5 * 5 = 25<br>
이것이 '분할 정복' 이 멋진 이유! <br>

<h6> [최악의 경우에는 시간 복잡도 O(N^2)이 된다] </h6>
<U>1</U> 2 3 4 5 6 7 8 9 10

**1** <U>2</U> 3 4 5 6 7 8 9 10

**1 2** <U>3</U> 4 5 6 7 8 9 10

분할정복의 이점을 사용하지 못하고 반복적으로 
10 + 9 ..+1 로 시간 복잡도 O(N^2)가 될 수 있다는것을 알아두어야한다. 

이미 정렬이 되어있는 경우에는 삽입 정렬이 매우 빠르다. 

그래서 문제의 특성에 따라 정렬을 잘 이용 할 줄 알아야한다~

References <br>
https://www.youtube.com/watch?v=gBcUO_6JXIA&list=PLRx0vPvlEmdDHxCvAQS1_6XV4deOwfVrz&index=6
