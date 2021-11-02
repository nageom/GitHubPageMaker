---
layout: post
current: post
cover:  assets/built/images/some/gist.png
navigation: True
title: 추천 목록, gist 보여주기
date: 2021-05-20 16:40:00
tags: [some]
class:
subclass: 
author: nageom
---
{% include some-table-of-contents.html %}
<h5>마크업 언어 사용 예시</h5>
1) 목록 보여줄때 (홀따음표 제거)   
>   "{"% include python-table-of-contents.html %}"  

_includes / oracle-table-of-contents.html 목록파일 추가해줘야함
2) gist 문서가져올때 (따음표 제거)   
> <'script src="https://gist.github.com/nageom/7dcd0b8fedc4ce5e44003d237e2fc0fa.js"></script'>   
   
   {'% gist nageom/7dcd0b8fedc4ce5e44003d237e2fc0fa %'} 는 해야할 것이 많다.. 예상치못한 에러때문에 시간을 
너무 허비해서 안쓰기로함. 
   
<script src="https://gist.github.com/nageom/7dcd0b8fedc4ce5e44003d237e2fc0fa.js"></script>

