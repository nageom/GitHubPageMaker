---
layout: post
current: post
cover: assets/built/images/algorithm/cover.png

navigation: True
title: <정렬> 정렬 알고리즘의 개요와 선택정렬(Select Sort)
date: 2021-06-22 00:14:00
tags: [algorithm]
class: post-template
subclass: 'post'
author: nageom
---
* * *
> <h3>알고리즘의 시작, 정렬 </h3>

<h6>왜 알고리즘 공부는 정렬부터할까?</h6>
정력만큼 알고리즘의 효율성 차이를 극명하게 보여주는 것이 없기 때문이다.<br>

비효율 정렬 -> 효율 정렬 순으로 공부! <br>

<h6>[가장 작은 거을 선택해서 제일 앞으로 보내면 어떨까?]</h6>
(구현하긴 쉽지만 효율적이진 않다)<br>

1 10 5 8 7 6 4 3 2 9<br>
1 2 5 8 7 6 4 3 10 9<br><br>

<h6> 구현해보자 </h6>
~~~javascript
//선택정렬  
int main(void) {


	int i, j, min, index, temp;
	int array[10]= {1,10,5,8,7,6,4,3,2,9};
	int arraySize = sizeof(array)/sizeof(int);
	

	for (i=0; i<10; i++) {
		min = 9999; //모든 원소들보다 큰 숫자
		for (j=i; j< arraySize; j++) {
			if (min > array[j] ) {
				min = array[j];
				index = j;
			}
			
		} 
		temp = array[i];
		array[i] = array[index];
		array[index] = temp;
		
		
	}
	for (i=0; i<10; i++) {
		printf("%d ", array[i]);
	}
	return 0;



}
~~~




<h6>[선택 정렬의 시간 복잡도 O(N^2) ]</h6>
int arr[] = {1 10 5 8 7 6 4 3 2 9} 를 정렬하기위해 비교하는 횟수<br>
10 + 9 + 8 + 7 + .. + 1<br>
=> 등차수열 공식으로 봤을 때<br>
10* (10+1)/2 = 55 번의 비교연산을 하게 된다.<br>
=> N * (N+1)/2<br>
일반적으로 컴퓨터에서는 N이 굉장히 큰 수라는 가정하에<br>
2로 나눈값이 별다른 큰 의미가 없다고 보고 간단하게 나누고 더하는 연산을 무시한다<br>
=> N*N 으로 표기<br>
=> O(N*N)  <br>
이 때 사용하는 것이 **'빅오 표기법(big-O notation)'** <br>
<U>특정한 알고리즘의 수행시간을 가장 간략하게 표기하는것 </U><br>
그리하여 선택 정렬의 시간 복잡도가 O(N^2)라 말한다.<br><br>

x값 처리할 데이터가 많을수록 연산 횟수가 엄청나게 증가한다. <br>
x제곱 그래프 
![ex_screenshot](../../assets/built/images/algorithm/sort/select sort.png)


References<br> 
https://www.youtube.com/watch?v=8ZiSzteFRYc&list=PLRx0vPvlEmdDHxCvAQS1_6XV4deOwfVrz&index=2 <br>
강의 최고시다..<br><br>

사진<br>
https://ko.depositphotos.com/10608715/stock-illustration-drawing-of-graph-on-squared.html
