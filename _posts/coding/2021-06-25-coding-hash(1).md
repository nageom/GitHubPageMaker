---
layout: post
current: post
cover: assets/built/images/coding/cover_coding.jpg

navigation: True
title: <프로그래머스> 해시(Hash)  Level 2 위장문제 (1)
date: 2021-06-25 00:14:00
tags: [coding]
class: post-template
subclass: 'post'
author: nageom
---
<h6> 프로그래머스 > 해시 > 위장문제</h6>
경우의 수를 구하는 문제인데 <br>
나는 경우의 수를 구하는게 너무 약해서 도와줘요 구글! 을 했다 <br>
옷 경우의 수 구하기..  <br>

> 상의 = 파란티, 빨강티 <br>
하의 = 바지, 치마, 레깅스  <br>

같은 타입은 겹쳐입지 않으며, 뭐라도 최소 한장 걸치는 것이 목적인 경우들을 구해봤다  <br>
파란티 + 바지 <br>
&nbsp; &nbsp; &nbsp; &nbsp;  &nbsp; &nbsp; &nbsp; &nbsp; + 치마 <br>
&nbsp; &nbsp; &nbsp; &nbsp;  &nbsp; &nbsp; &nbsp; &nbsp; + 레깅스 <br>
빨강티 + 바지 <br>
&nbsp; &nbsp; &nbsp; &nbsp;  &nbsp; &nbsp; &nbsp; &nbsp; + 치마 <br>
&nbsp; &nbsp; &nbsp; &nbsp;  &nbsp; &nbsp; &nbsp; &nbsp; + 레깅스 <br>
상의 안입기 + 바지 <br>
&nbsp; &nbsp; &nbsp; &nbsp;  &nbsp; &nbsp; &nbsp; &nbsp; + 치마 <br>
&nbsp; &nbsp; &nbsp; &nbsp;  &nbsp; &nbsp; &nbsp; &nbsp; + 레깅스 <br>

이렇게 총 9개가 나온다. <br>
그럼 (상의 2개 + 안입는 경우) * (하의 3개 + 안입는 경우)  ... <br>
의 공식을 뽑아낼 수 있다. <br>

그리하여 {/{"옷 ", "옷 타입"}/} 의 형태인 2차 배열에서 <br>
각 옷 타입의 수를 구해 경우의 수를 반환하는 식의 코드를 짰다.<br>

~~~ javascript
import java.util.*;
class Solution {
    public int solution(String[][] clothes) {
        int answer = 1;
        HashMap<String, Integer> map= new HashMap<String, Integer>();
       
       //map에 <"face", 0> 이렇게 중복값 없이 넣어준다. 
        for (int i=0; i< clothes.length; i++) {
            map.put(clothes[i][1], 0 );       
        }
        // 배열과 직접 비교하며 +1로 옷 타입마다 몇개인지 세어 map에 다시 넣어준다. 
         for(String key: map.keySet()) {
            for (int i=0; i<clothes.length; i++) {
                if ( key.equals(clothes[i][1]) ) {
                    int tmp = map.get(key);
                    tmp +=1;
                    map.put(key, tmp);
                }
            
            }
        }
        //경우의 수 구하기 :  (상의 + 안 입는 경우 ) * (하의 + 안 입는 경우 )
        for (int value : map.values()) {
            answer *= value+1;
        
        }
       
        
        return answer-1;
    }
}

~~~



<br><br>
커버사진 출처 프로그래머스 