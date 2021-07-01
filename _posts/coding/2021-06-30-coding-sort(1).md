---
layout: post
current: post
cover: assets/built/images/coding/cover_coding.jpg

navigation: True
title: <프로그래머스> 정렬  Level 1 K번째 수(1)
date: 2021-06-30 00:14:00
tags: [coding]
class: post-template
subclass: 'post'
author: nageom
---
* * *
**프로그래머스 > 정렬 > K번째 수**

문제 설명
배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면

array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
2에서 나온 배열의 3번째 숫자는 5입니다.
배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

제한사항
array의 길이는 1 이상 100 이하입니다.
array의 각 원소는 1 이상 100 이하입니다.
commands의 길이는 1 이상 50 이하입니다.
commands의 각 원소는 길이가 3입니다.

![ex_screenshot](../../assets/built/images/coding/sort(1)_1.png)

입출력 예 설명
[1, 5, 2, 6, 3, 7, 4]를 2번째부터 5번째까지 자른 후 정렬합니다. [2, 3, 5, 6]의 세 번째 숫자는 5입니다.
[1, 5, 2, 6, 3, 7, 4]를 4번째부터 4번째까지 자른 후 정렬합니다. [6]의 첫 번째 숫자는 6입니다.
[1, 5, 2, 6, 3, 7, 4]를 1번째부터 7번째까지 자릅니다. [1, 2, 3, 4, 5, 6, 7]의 세 번째 숫자는 3입니다.

**[지저분하게 완성된 첫 풀이]**<br>
테스트에 통화는 했지만 풀면서 이게 아님을 느꼈지만 일단 진행했고 더 간략하게 짤 수 있었을텐데 하는 아쉬움이 많이 남았다.
**이런 코딩을 한 이유**<br>
1) 주어진 배열 array의 i와 j 범위를 다른 배열안에 넣어 정렬을 해야하는데 일반 배열은 크기를 정해줘야함으로
i와 j의 범위가 다 다르기 때문에 크기를 정할 필요없는 ArrayList를 골랐다.<br>
   2) 바보같이 answer의 배열 크기를 모를거라 생각하고 k값을 넣어줄 배열 또한 ArrayList를 골랐다.
    
그리하여 첫 제출한 코드 

~~~ javascript
package sort;
import java.util.*;
public class K {
	public static int[] solution(int[] array, int[][] commands) {
        int[] answer = null;
        List<Integer> answerTmp = new ArrayList<Integer>();

        List<Integer> arr = null;
        int i=0;
        for (; i< commands.length; i ++) {
        	arr = new ArrayList<Integer>();
        	
            int start =commands[i][0];
            int end = commands[i][1];
            int k = commands[i][2];
       
            for (int t=start-1; t<end; t++) {
                arr.add(array[t]);
              
            }   
            Collections.sort(arr);
            //정렬
       
            answerTmp.add(arr.get(k-1));   
        }
 
        i =0;
        answer = new int[answerTmp.size()];
        for (int a : answerTmp) {
        	answer[i++] = a;
        }
        
        return answer;
    }
	
	public static void main(String[] args) {
		int[] array = {1,5,2,6,3,7,4};
		int[][] commands= [[2,5,3], [4,4,1], [1, 7, 3]]; // 블로그 업로드 과정에서 에러가 나서 중괄호를 대괄호로 수정한것이니 참고하세요.
		int[] answer = solution(array, commands);
		for (int a : answer ) {
			System.out.println(a+ " ");
		}
	}
}
~~~

**[이 후 두번째 풀이]**<br>
1) 주어진 i~k 의 범위가 commands배열의 크기를 넘지 않을 것을 깨닫고 <br>
그 범위를 담을 tmp배열의 크기를 정해주고<br>
2) Arrays.copyOfRange()를 이용하여 배열안에 i ~ k 범위를 담아주었다.<br>
그로인해 쓸데없는 for문 하나를 없앨 수 있었다.<br>
   
물 흐르듯 코드가 간략해졌다. <br>
~~~javascript
import java.util.*;
class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];
        int[] tmp = new int[commands.length];
        int index =0;
        
        for (int i=0; i< commands.length; i ++) {
            int start =commands[i][0];
            int end = commands[i][1];
            int k = commands[i][2];
       
            tmp = Arrays.copyOfRange(array, start-1, end);
            
            Arrays.sort(tmp);
            answer[i] = tmp[k-1];
            //정렬
         
        }
        
        
        
        return answer;
        
    }
}
~~~

<br><br>
커버사진 출처 프로그래머스 