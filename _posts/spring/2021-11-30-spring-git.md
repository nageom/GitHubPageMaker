---
layout: post
current: post
cover:  assets/built/images/spring/git.png
navigation: True
title: 깃 협업을 해보자 
date: 2021-05-25 00:28:00
tags: [Spring]
class: post-template
subclass: 'post tag-python'
author: nageom
---

이제 깃허브에 소스파일을 올린적은 있지만 협업에 사용해본적은 없다. 
취업기념 깃 공부 뿌웽웽

(레파지토리 주인)

우선적으로  알아야할 개념.<br>
깃 허브 레파지토리는 공유할 프로젝트를 올려두는 공간 (프로젝트 하나당 레파지토리 하나 )<br>
깃은 내 소스코드를 이 레파지토리에 올려주는 바쁜 친구<br>
그래서 소스코드 올린다고 할 때, 깃허브에 가입하고 레파지토리를 만들어주고, 깃도 설치해준다.<br>

과정을 보기전에 전체적인 흐름을 보고 시작하자.<br>
내 PC의 workspace 내의 프로젝트가 바로 레파지토리에 연결되는 것이 아니라<br>
깃 저장소라는 공간을 만들고 이 깃 저장소가 레파지토리와 연결되는 것이다.<br>
그래서,<br>
1) 깃 저장소를 만들고(git init)<br>
2) workspace -> 깃 저장소 이렇게 올라간다. (commit)<br>
   이때 중간에 장바구니에 add로 중간중간 공유 파일을 담아주고 깃 저장소에 올림<br>
3) 깃 저장소 -> 레파지토리 (push)<br>



시작은 달콤하게 깃허브 페이지에서 <br>
- 레파지토리 생성<br>
- Settings / Mange access / Invite a collaborator 에서 조원 초대<br>
- 깃설치 git-scm.com<br>
- Git bash 오픈 / cd 프로젝트 폴더<br>


**Git bash**<br>
- 사용자 등록<br>
  git config --global user.name "nageom"<br>
  git config --global user.email "nageom1123@naver.com" //깃허브 아이디<br>

**내 컴퓨터에 깃 저장소 만들기**<br>
**Git Bash** (위치 : 프로젝트 폴더 내)<br>
- git init 명령어<br>
  그러면 폴더 내에 .git이 생성됨을 확인할 수 있다. (깃 저장소)<br>

**공유할 파일 외의 파일 제외** (.gitignore 파일 생성)<br>
- git status 명령어<br>
  (git로 공유한 파일과 공유할 장바구니 내부를 볼 수 있다. )<br>

- code .  명령어 (visual code가 열림)<br>

- vs에서 .gitignore 파일 생성 (깃에게 제외할 파일을 알려줌)<br>
- .gitignore 파일에 제외할 파일 이름 적음<br>
  bin<br>
  .classpath<br>
  .project<br>
  .settings<br>
  이런식<br>
- git status로 파일 이름 하나 적을때마다 공유하는 파일 이름 확인 (빨간글씨)<br>

**파일 ->  장바구니** (git add)<br>
- git add .gitignore<br>
- git add .  (전부 공유한다. )<br>

**장바구니 -> 깃 저장소** (git commit -m)<br>
- git commit -m "first commit"<br>

**깃 저장소 + 레파지토리 연동**(git remote add) <br>
-  git remote add origin https://githumb.com/내아이디/레파지토리이름.git (레파지토리 주소)<br>
   (이때, origin은 변수명이다. 뒤의 주소를 origin 으로 기억해라 라는뜻)<br>

- 확인<br>
  git remote -v<br>
  이때, (fetch), (push) 두개 뜸<br>
- 그럼 연결은 끝<br>

**깃 저장소 -> 레파지토리**<br>
- git push origin master<br>
  origin변수 주소 안에 넣어라<br>

- 로그인 했는데도 안될때<br>
  git config --system --unset-all credential.helper<br>
  (로그인 정보 없애기)<br>

===============================================<br>
**연결 끝한 이후**<br>
- git add .<br>
- git commit -m "commit"<br>
- git push origin master <br>


> 이제 다른 사람 레파지토리에서 내려받아 사용하는 경우 


**레파지토리 소스코드 내려받기**<br>

**1) 내 workspace에 폴더 하나 생성 (프로젝트가 될 폴더)**<br>

**2) 내 pc에 저장소 만듦**(git init)<br>
( 공유는 저장소만 가능하다. 받을 소스코드는 우선 깃 저장소에 들어가게 해야한다.)<br>
- git init<br>

**3) 내 저장소와 공유할 레파지토리 연결** (git remote)<br>
- git remote add origin https://github.com/조장아이디/레파지토리이름.git<br>

**가져오기**(git pull) <br>
- git pull origin master<br>

--------------위의 두 과정 또는 cmd에서 git clone https://github.com/조장아이디/레파지토리이름.git  프로젝트가될폴더이름<br>
ex )  git clone https://github.com/nageom/salemarket.git salemarket<br>
GitBash 위치는 salemarket 위<br>


**이클립스 업뎃**<br>
File/import<br>
General / Projects from Folder or Archive<br>
- next<br>
- import 할 경로를 바꿔줌<br>

라이브러리 Build Path는 내가 해줘야함. / 라이브러리들 우클릭 Build Path<br>


=====================================================<br>
연결 이 후,<br>
변경사항을 받아올때도<br>
- git pull origin master<br>

내 변경사항 올릴때도<br>
git push origin master<br>
(안될때는 pull 먼저 해줌(최신 버전으로 업뎃 하고 내꺼 올리는식)  )<br>


=======================================================<br>
> 회사에서 회사 master말고 내 브랜치를 만들어 push 할 경우<br>

**git checkout -b freshman**<br>
내 브랜치 만듦 (GitBash 위치: 프로젝트 내에서 명령)<br>
(freshman은 브랜치 이름)<br>
- 이제 push 될 브랜치가 master에서 freshman으로 바뀜<br>

**git push origin freshman**<br>
- 올림<br>

**이제 내 코드 봐달라고 request**<br>
- 회사 레파지토리에 접속해보면 내가 push한 내역을 Compare & pull request 하게 되어있음<br>
- 클릭<br>
- 멘트 블라블라  -> Create pull request<br>

Pull requests가 생김<br>
- 이건 회사에서 확인하고 Merge ㅎㅎ <br>



































