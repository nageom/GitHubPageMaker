---
layout: post
current: post
cover: assets/built/images/coding/cover_coding.jpg

navigation: True
title: <프로그래머스> 완전탐색  Level 2 소수찾기(2)
date: 2021-07-03 00:14:00
tags: [coding]
class: post-template
subclass: 'post'
author: nageom
---
* * *
**프로그래머스 > 완전탐색 > 소수찾기**

문제 설명<br>
한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

제한사항
numbers는 길이 1 이상 7 이하인 문자열입니다.
numbers는 0~9까지 숫자만으로 이루어져 있습니다.
"013"은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.<br><br>
**입출력 예**<br>
numbers	return<br>
"17" &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;	3<br>
"011" &nbsp; &nbsp; &nbsp; &nbsp;	2<br><br>
입출력 예 설명<br>
예제 #1<br>
[1, 7]으로는 소수 [7, 17, 71]를 만들 수 있습니다.<br>

예제 #2<br>
[0, 1, 1]으로는 소수 [11, 101]를 만들 수 있습니다.

11과 011은 같은 숫자로 취급합니다.

<h6>[풀이과정]</h6>
   
순열 알고리즘과 제곱근을 이용한 소수판별법을 사용해 코드를 작성했다. <br>
정말 내 머리로는 힘들어서 
 https://hidelookit.tistory.com/67 이 분의 힘을 빌렸다.. 파워풀..



**[코드를 살펴보자]**
~~~ javascript
package exhaustiveSearch;
import java.util.*;
public class PrimeNum {
	private static int cnt = 0;
    private static String[] map;
    private static String[] result;
    private static boolean[] visit;
    private static HashSet<Integer> list;

	public static int solution(String numbers) {
		int answer = 0;

        visit = new boolean[numbers.length()];
        map = new String[numbers.length()];
        map = numbers.split("");

        list = new HashSet();

        for (int i=1; i<=numbers.length(); i++) {
            result = new String[i];
            cycle(0, i, numbers.length());
        }

        return list.size();
	    
	    
	}
	
	
	 public static void cycle(int start, int end, int length) {

	        if (start == end) {
	            findPrime();
	        } else {

	            for (int i=0; i<length; i++) {
	                if (!visit[i]) { //true로 바꿔서 배열 2번째, 3번째 값들을 하나씩 배열에 넣어주는 역할
	                    visit[i] = true;
	                    result[start] = map[i]; // result[0]=[1], result[1]=[7] 
	                    cycle(start+1, end, length); //findPrime에 도달하기위해 start++
	                    visit[i] = false;
	                }
	            }

	        }

	    }

	public static void findPrime() {

	        // 숫자로 변환
	        String str = "";
	        for(int i=0; i<result.length; i++)
	            str += result[i];
	        int num = Integer.parseInt(str);

	        // 예외 처리
	        if(num == 1 || num == 0)
	            return;

	        // 소수 인지 검사
	        boolean flag = false;
	        for(int i=2; i<=Math.sqrt(num); i++){  //Math.sqrt()는 num의 제곱근을 구해주는 메서드이다. 
	            if(num % i == 0)
	            	
	                flag = true;
	        }

	        if(!flag)
	            list.add(num);
	    }
	
	public static void main(String[] args) {
		String numbers = "17";
		String numbers2 = "011";
		
		int result = solution(numbers);
		
		System.out.println("result : "+ result);
	}
}


~~~
**배운것**<br>
Math.sqrt()는 num의 제곱근을 구해주는 메서드를 처음 알았다. <br>
또 private static boolean[] visit 배열의 활용을 공부하니
앞으로의 코딩에도 유용하게 사용될 것 같다. 






<br><br>
커버사진 출처 프로그래머스 