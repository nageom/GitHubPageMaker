---
layout: post
current: post
cover: assets/built/images/algorithm/cover.png

navigation: True
title: <정렬>버블정렬(Bubble Sort)
date: 2021-06-22 00:14:00
tags: [algorithm]
class: post-template
subclass: 'post'
author: nageom
---
* * *
> <h4>버블정렬 </h4>

<h6>[옆에 있는 값과 비교해서 더 작은 값을 앞으로 보내는 방법]</h6>
직관적이고 쉽게 구현할 수 있지만 정렬 알고리즘 중에서 가장 비효율적인 알고리즘이다!<br>
<U>1 10</U> 5 8 7 6 4 3 2 9  &nbsp; <- 두개를 한 묶음으로 비교<br>
1 <U>10 5 </U>8 7 6 4 3 2 9 <br>
1 10 <U>5 8 </U> 7 6 4 3 2 9 <br><br>
(1회전)<br>
1 5 8 7 6 4 3 2 9 10 <- 가장 큰 값이 맨 뒤로 간다<br>
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;그래서 1회전 반복때마다 반복 횟수를 줄여준다.<br>
(2회전)<br>
1 5 7 6 4 3 2 8 9 10  <br><br>
결과<br>
1 2 3 4 5 6 7 8 9 10<br><br>

<h6> 구현해보자 </h6>
~~~javascript
#include <stdio.h>
int main(void) {
    int i, j, tmp;
    int arrSize = 10;
    int arr[arrSize] = {1,10,5,8,7,6,4,3,2,9};
    for (i=0; i<arrSize; i++) {

        for (j=0; j<arrSize-i; j++) {
            if (arr[j]> arr[j+1]) {
                tmp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1]= tmp;
            }
        }
    }
    for (i =0; i<arrSize; i++) {
        printf("%d ", arr[i]);
    }
    return 0;
}
~~~



<h6>[버블 정렬의 시간 복잡도 O(N^2) ]</h6>
<U>1 10</U> 5 8 7 6 4 3 2 9<br>
=> 10 + 9 + ... + 1<br>
=> 10 + 9 + ... + 1<br>
=> 등차수열<br>
=> N* (N+1)/2<br>
=> O(N^2)<br>
<h6>선택정렬과 동일한 시간 복잡도이지만 왜 가장 비효율적인 정렬이라 하지?</h6> <br>
선택정렬은 가장 작은 데이터를 골라 마지막에 자리 이동을 한다. <br>즉, 1회전에 자리이동 1회<br> 
버블정렬은 매번 교체를 해줘야하기 때문에 더 오랜 시간이 걸린다. <br> 즉, 1회전에 자리이동 여러번  <br>
그래서 정렬중 가장 비효율적 정렬이라 함! <br><br>

References <br>
https://www.youtube.com/watch?v=EZN0Irp2aPs&list=PLRx0vPvlEmdDHxCvAQS1_6XV4deOwfVrz&index=3<br>

