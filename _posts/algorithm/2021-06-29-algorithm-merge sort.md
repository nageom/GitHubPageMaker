---
layout: post
current: post
cover: assets/built/images/algorithm/cover.png

navigation: True
title: <정렬> 병합 정렬(Merge Sort)
date: 2021-06-29 00:14:00
tags: [algorithm]
class: post-template
subclass: 'post'
author: nageom
---
* * *

<h6>[ 일단 반으로 나누고 나중에 합쳐서 정렬해보자 ]</h6>
퀵 정렬과 다르게 피벗 값이 없고 무조건 반으로 모두 나누고 합하면서 정렬한다는 방법이다.<br>


![ex_screenshot](../../assets/built/images/algorithm/sort/merge sort(1).png)

실제로 각 다른 배열을 갖는것이아니라 논리적으로 그렇다고 생각하고 그림처럼 정렬시킨다.<br>
각 하나로 만들고 분할 병합하며 정렬하는 방식이다.<br>

더 자세히 코드느낌으로 보자면<br>
![ex_screenshot](../../assets/built/images/algorithm/sort/merge sort(2).png)
나누어진 두 배열을 비교하며 작은 값을 <U>k인덱스</U>에 하나씩 집어넣는다. <br>
이 때 실제로 <U>k</U>은 새로운 배열이 아니라 <U>i</U>와 같은 배열이다.<br>

<h6>[병합 정렬의 시간 복잡도 O(N* log2N) ]</h6>

![ex_screenshot](../../assets/built/images/algorithm/sort/merge sort(3).png)
배열의 (너비) N *  (높이) log2 N = O(N*log2 N) 시간복잡도가 나온다. <br>


어째서 정렬에 높이 log2 N 밖에 안나오냐라는 질문에는 이미 정렬된 두 배열을 정렬하기 때문이라고 답할 수 있다. <br>

실제로 나누어진 두 배열을 하나로 합하며 정렬해 나갈때 N번의 반복만 수행이 된다. <br>
내가 이해한 루트로 설명해보자면 <br>

1번째 줄에서 2번째 줄로 분할병합 할 때, 먼저 **{6,5}  {5,8}** <br>
1회전->  i(0)과 j(0)비교<br> 
2회전-> i(0)과 j(1)비교<br>
3회전-> i(1)과 j(0)비교<br>
4회전-> i(1)과 j(1)비교<br>
총 4회 -> 배열의 총 크기만큼만 수행된다. <br>
그렇다면 그 옆 배열 **{3,5}, {1,9}**의 분할병합에서도 <U>4회의 반복</U>이 될것이고<br>
즉, 그림에 한 줄 **N번의 수행**을 한다라는것을 알 수 있다. <br>



시간 복잡도가 퀵 정렬과 같은데 다른 점이라 하면<br>
**퀵 정렬**은 정렬 알고리즘 중 가장 빠른 속도를 자랑하지만 최악의 경우에는 O(N^2)가 될 수 있는 정렬이고,<br>
**병합 정렬**은 최악의 상황에서도 평균 O(N*logN)을 보장할 수 있다는 것이 큰 장점으로 쓰인다. <br>


<h6>[코드를 살펴보자]</h6>
~~~ javascript

#include <stdio.h>

int number =8; 
int sorted[8]; // 정렬 배열은 반드시 전역 변수로 선언
 
//정렬된 배열을 담을 뱅
// 논리적으로 둘로 나누어진 i, j 배열을 정렬하며 합치는 메서드 merge 
										//n은 j의 끝 인덱스 
void merge(int a[], int m, int middle, int n ) {
	
	int i=m; // 왼쪽배열 시작점 
	int j = middle+1; // 한칸 띄움 
	int k=m; //정렬된 배열 
	//k는 사실상 i와 동일한 위치를 가진다. 
	// 그림은 정렬 전 배열과 정렬 후의 배열을 따로 두었지만
	// 실제로는 하나의 배열을 사용중  
	
	//작은 순서대로 배열에 삽입 
	while (i <=middle && j <= n ) {
		if (a[i] <= a[j]) {
			sorted[k]= a[i];
			i++;
		}else {
			sorted[k]= a[j];
			j++;
		}
		k++;	
	}
	
	//남은 데이터도 삽입 
	if (i>middle) {
		for (int t=j; t<=n; t++) {
			sorted[k]= a[t];
			k++;
		}
		
	} else {
		for (int t=i; t<=middle; t++) {
			sorted[k] = a[t];
			k++;
			
		}
	}
	// 정렬된 배열을 삽입
	for(int t=m; t<=n; t++) {
		a[t] = sorted[t];
	} 
	
	
}
 
void mergeSort(int a[], int m, int n) {
	//크기가 1보다 큰 경우
	if(m <n) {
		int middle = (m+n) /2;
		mergeSort(a,m,middle);
		mergeSort(a, middle+1, n );
		merge(a, m, middle, n);
	}
}
int main(void) {
	int array[number] = {7,6,5,8,3,5,9,2} ;
	mergeSort(array, 0, number-1);
	for (int i=0; i<number; i++ ) {
		printf("%d ", array[i]);
	}
}
~~~
References <br>
강의영상<br>
https://www.youtube.com/watch?v=ctkuGoJPmAE&list=PLRx0vPvlEmdDHxCvAQS1_6XV4deOwfVrz&index=8<br>
사진첨부<br>
https://blog.naver.com/ndb796/221227934987