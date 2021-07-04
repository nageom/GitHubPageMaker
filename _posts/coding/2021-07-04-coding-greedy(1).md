---
layout: post
current: post
cover: assets/built/images/coding/cover_coding.jpg

navigation: True
title: <프로그래머스> 탐욕법 체육복
date: 2021-07-04 00:14:00
tags: [coding]
class: post-template
subclass: 'post'
author: nageom
---
* * *
**프로그래머스 > 탐욕법 > 체육법**

문제 설명<br>
점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다. 예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다. 체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다.

전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.
<br><br>
제한사항<br>
전체 학생의 수는 2명 이상 30명 이하입니다.
체육복을 도난당한 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
여벌의 체육복을 가져온 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있습니다.
여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.

![ex_screenshot](../../assets/built/images/coding/greedy(1)_1.png)


입출력 예 설명<br>
예제 #1<br>
1번 학생이 2번 학생에게 체육복을 빌려주고, 3번 학생이나 5번 학생이 4번 학생에게 체육복을 빌려주면 학생 5명이 체육수업을 들을 수 있습니다.
<br>
예제 #2<br>
3번 학생이 2번 학생이나 4번 학생에게 체육복을 빌려주면 학생 4명이 체육수업을 들을 수 있습니다.




<h6>[풀이과정]</h6>
n 크기의 boolean[] flag를 만들어
1. lost는 false 나머지는 true 
2. reserve 데이터의 앞, 뒤를 확인하며 false를 true로 바꿔줌.

나는 막히는 테스트케이스가 딱 두가지 있었는데<br>
**n=5; lost = {3,5}; reserve={2,4};의 경우**<br>
답 5<br>
s
또는 <br>

**n=5; lost={2,3,4}; reserve= {1,2,3};** <br>
답 4<br><br>
이때는 도둑맞은 학생이 여벌을 갖을 경우에는 남을 빌려주지않고 본인이 입는다는 조건을 충족시켜야한다. 
이 경우에는 나는 겹치는 수를 reserve에서 0으로 만들고 코드에 0인 경우에 대한 조건문을 추가했다. 
배열 안에 특정 원소를 가지고 있는지 확인 할 수 있는 메서드 Arrays.stream(reserve).anyMatch(i->i==a)를 사용했다.<br>
이외의 같은 기능을 하는 메서드는 https://www.delftstack.com/ko/howto/java/java-array-contains-int 
 이 분이 잘 정리 하셨다. <br>

하지만 다른 분들의 코드에 비해 아주 길었고.. 보기 편한 코드는 아니기 때문에 
한번 더 재코딩해서 올릴 예정이다. <br>
**[코드를 살펴보자]**
~~~ javascript
package greedy;

import java.util.*;


public class Gym {
	public static int solution(int n, int[] lost, int[] reserve) {
        int answer = -1;
        
        boolean[] flag = new boolean[n+1]; 
        Arrays.fill(flag,true);    // [true, true, true, true, true]
        
        Arrays.sort(lost);
        Arrays.sort(reserve);
        for (int i=0; i<lost.length; i++) {
        	flag[lost[i]]= false;   
        }
        System.out.println("lost는 false----------");
        for (boolean a : flag) {
        	System.out.println(" "+ a);
        }
        
        System.out.println("도둑맞았지만 여벌이 남아있는 학생 true-----------");
        for(int a : lost) {
        	if (Arrays.stream(reserve).anyMatch(i->i==a)) {       		
        		flag[a] = true;	 
        		for (int t =0; t<reserve.length; t++) {
        			if (reserve[t]==a) {
        				reserve[t]=0;	
        			}
        			
        		}
        		
        	}
        }
        for (boolean a : flag) {
        	System.out.println(" "+ a);
        }
       
       // System.out.println("start");
        
        for (int i=0; i<reserve.length; i++) {
        	int prev = reserve[i]-1;
        	int post= reserve[i]+1;
        	
        	//도둑맞았지만 여벌이 남아있는 학생
        	if (reserve[i] == 0) {
        		continue;
        	}
        	//reserve[0]이 1일경우 뒤에 갚만 비교
        	if (i==0 && reserve[0]==1) {
        		if (flag[post]==false) {
        			flag[post]=true;
        		}     		
        		
        		continue;
        	}
        	
        	//reserve의 마지막배열이 flag의 마지막일때 
        	// 자신의 앞만 비교
        	if(i == reserve.length-1) {
        		if (reserve[i] == flag.length-1) {
        			if(flag[prev] == false) {
            			flag[prev]=true;
        			}
        			break;    		
        		}
        		
        	}
   	
        	if(flag[prev]==false) {
        		flag[prev]=true;   		
        	}else if (flag[post]==false) {	
        		flag[post]=true;
        		
        	}
        }
        System.out.println("결과 ==============");
        for (boolean a : flag) {
        	System.out.println(" "+ a);
        }
    
        //int count=-1;
        for (int i =0; i<flag.length; i++) {
        	if(flag[i]==true) {
        		answer++;
        	}
        }
        return answer;
    }

	public static void main(String[] args) {
		
		int n= 5;
		int[] lost= {2,4};
		int[] reserve = {1,3,5};
		//5나와야함 
		int result = solution(n, lost, reserve);
		
		System.out.println("Result : "+ result );

	}
}


~~~







<br><br>
커버사진 출처 프로그래머스 