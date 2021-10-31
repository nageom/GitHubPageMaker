---
layout: post
current: post
cover: assets/built/images/algorithm/cover.png

navigation: True
title: <정렬> 힙 정렬(Heap Sort)
date: 2021-07-12 00:14:00
tags: [algorithm]
class: post-template
subclass: 'post'
author: nageom
---
* * *
**힙이란??**
최댓값이나 최솟값을 찾아내는 연산을 빠르게 하기위해 고안된 완전 이진트리를 기본으로 한 자료구조입니다. 
최소힙, 최대힙이 있는데 트리 루트가 최솟값인지, 최댓값인지에 따라 구분된다.<br>

**트리란 ??**
부모와 자식 노드로 구성된 형태의 그래프이다. 
이진트리는 한 부모노드가 자식을 두개만 갖는 경우를 말한다. 
완전 이진트리는 모든 부모노드가 자식을 두개씩 다 가지고 있고
왼쪽부터 노드가 채워져있어야한다.<br>

완전 이진트리가 아닌 경우 
![ex_screenshot](../../assets/built/images/algorithm/sort/heap(1)_2.png)

**[실제 코드를 짤때 알고있어야할 힙 구조의 배열저장 형식  ]**
![ex_screenshot](../../assets/built/images/algorithm/sort/heap(1)_4.jpg)



<h6>힙의 높이 (h) = logN 이다. (간선의 수)</h6>
루트노드에서 한 칸씩 내려올때마다 N의 크기가 두배씩 늘어나는데 
몇 번 늘어나면 N개가 되느냐를 생각해보면 이해하기 쉽다.
![ex_screenshot](../../assets/built/images/algorithm/sort/heap(1)_3.png)



최대힙 (Max-Heapify)
이진트리 하나씩 부모노드와 자식노드들을 비교해서 가장 큰 값이 부모노드의 값이 되도록 하여
최상위 루트 노트의 값이 가장 크고 내려갈수록 작아지는 구조의 힙

<h6>최대힙의 수행시간</h6>
n을 하위 트리의 노드의 개수라고 할 때,
노드의 값을 바꿀 때 수행시간 : O(1)    //단순히 값을 이동시키기 때문에 상수시간이 가능하다. 
힙의 높이 O(h) = O(logN) 
따라서 전체 수행시간은 O(logN)이다.
<br>
참고강의 https://www.youtube.com/watch?v=ehNVf2Bcm2Q








