---
layout: post
current: post
cover: assets/built/images/coding/cover_coding.jpg

navigation: True
title: <프로그래머스> 완전탐색 카펫(3)
date: 2021-07-04 00:14:00
tags: [coding]
class: post-template
subclass: 'post'
author: nageom
---
* * *
**프로그래머스 > 완전탐색 > 카펫**<br>
Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 노란색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.
![ex_screenshot](../../assets/built/images/coding/exhaustive search(3)_1.png)
Leo는 집으로 돌아와서 아까 본 카펫의 노란색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다.

Leo가 본 카펫에서 갈색 격자의 수 brown, 노란색 격자의 수 yellow가 매개변수로 주어질 때 카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.

제한사항
갈색 격자의 수 brown은 8 이상 5,000 이하인 자연수입니다.
노란색 격자의 수 yellow는 1 이상 2,000,000 이하인 자연수입니다.
카펫의 가로 길이는 세로 길이와 같거나, 세로 길이보다 깁니다.

![ex_screenshot](../../assets/built/images/coding/exhaustive search(3)_2.png)


<h6>[풀이과정]</h6>
yellow의 가로세로 모양에 따라 brown 의 개수가 달라진다. 
yellow의 모양을 가늠할 수는 없지만 결국 네모를 만들것이라는 것은 항상 동일하다. 
네모의 가로 세로는 yellow의 약수일 수밖에 없다. 
그래서 yellow의 약수를 구하고 그때마다 구해지는 brown 값을 주어진 brown 값과 비교하여 결과를 도출했다. 

전 테스트에서 알게된 Math.sqrt() 함수가 도움이 됐다. 

**[코드를 살펴보자]**
~~~ javascript
import java.util.*;
class Solution {
    public int[] solution(int brown, int yellow) {
        int[] answer = new int[2];
        
        int tmp =0;
        boolean flag=false;
        for (int i=1; i<=Math.sqrt(yellow);i++ ) {
            if (yellow % i == 0) {
                tmp = yellow/i;
                flag = checkTrue(tmp, i, brown);
                if (flag == true){
                    answer[0]=tmp+2;
                    answer[1]=i+2;
                    break;
                }
            }     
            
        }    
        
        return answer;
    }
    
    public boolean checkTrue(int width,int height, int brown) {
        int make=( width*2 )+(height*2)+4;
        if(make == brown) {
            return true;
        }
        return false;
        
    }
    
}
~~~







<br><br>
커버사진 출처 프로그래머스 