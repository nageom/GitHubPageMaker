---
layout: post
current: post
cover: assets/built/images/coding/cover_coding.jpg

navigation: True
title: <프로그래머스> 정렬  Level 2 H-Index(3)
date: 2021-07-01 00:14:00
tags: [coding]
class: post-template
subclass: 'post'
author: nageom
---
* * *
**프로그래머스 > 정렬 > H-Index**
문제 설명
H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과1에 따르면, H-Index는 다음과 같이 구합니다.<br>
어떤 과학자가 발표한 논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h의 최댓값이 이 과학자의 H-Index입니다.<br>
어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

제한사항
과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
논문별 인용 횟수는 0회 이상 10,000회 이하입니다.
입출력 예
citations	return
[3, 0, 6, 1, 5]	3
입출력 예 설명
이 과학자가 발표한 논문의 수는 5편이고, 그중 3편의 논문은 3회 이상 인용되었습니다. 그리고 나머지 2편의 논문은 3회 이하 인용되었기 때문에 이 과학자의 H-Index는 3입니다.
**입출력 예**<br>
citations &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return<br>
[3,0,6,1,5] 3

입출력 예 설명
이 과학자가 발표한 논문의 수는 5편이고, 그중 3편의 논문은 3회 이상 인용되었습니다. 그리고 나머지 2편의 논문은 3회 이하 인용되었기 때문에 이 과학자의 H-Index는 3입니다.

이해하고나면 쉽지만 처음 문제를 읽으면 물음표를 찍을 문제였다. 
논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h의 최댓값이 이 과학자의 H-Index이다.

일단 나는 h가 citations의 길이를 넘기지 않으면서
최댓값으로 측정되어야한다 
그리고 값 h 이상의 h 개수이다라는 조건을 갖고 문제를 풀었다. 

그래서 h를 먼저 citations 길이에 맞추고 하나씩 줄여나가며 값을 비교했고
반복을 줄이기위해 Arrays.sort()를 이용해 오름차순된 정렬을 사용했다.

아, 그리고 나중에 안 사실인데 문제 조건에는 값 h이상의 h이상의 개수라고 되어있지만
밑에 내 코드를 보면 알겠지만
if(tmp >= k) 대신 if(tmp == k) 를 처음에 적었을때도 테스트를 모두 통과했던것으로 보아 
h이상의 h 개수가 조건인가보다.


**[코드를 살펴보자]**
~~~ javascript
import java.util.*;
class Solution {
    public int solution(int[] citations) {
        int answer = 0;
		//k는 0 이상, length이하
		int k = citations.length;
		
		Arrays.sort(citations);
		//0 1 3 5 6
		//87 56

		int tmp = 0;
		for (int i=0; i<citations.length; i++) {
			if (citations[i]>= k )  {
				//k이상이면 그 이후 데이터도 모두 k 이상
				tmp = citations.length-i;

				if(tmp >= k) {//tmp == k 의 조건에도 코드가 성공함
					break;
				}
			}
			k--;
			
		}
		
		answer = tmp;
		return answer;
		
    }
}
~~~




<br><br>
커버사진 출처 프로그래머스 