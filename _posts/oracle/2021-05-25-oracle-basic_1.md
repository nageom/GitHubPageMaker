---
layout: post
current: post
cover: assets/built/images/oracle.png
navigation: True
title: Oracle-basic_1
date: 2021-05-25 00:14:00
tags: [oracle]
class: post-template
subclass: 'post'
author: nageom
---
 {% include oracle-table-of-contents.html %}
 * * *
1) RDBMS : 관계형 데이터베이스 관리 시스템
 
> 데이터베이스의 종류: 네트워크형, 계층형, 관계형, NoSQL DB   
그 중, 시각적으로 쉽게 데이터를 확인 할 수 있는 장점으로 가장 많이 사용되는 형태의 데이터베이스를
RDB_관계형 데이터베이스라고 합니다.

![ex_screenshot](./assets/built/images/basicTable.png)

행과열 조합으로 테이블 형태를 띄고있으며 각 테이블과 테이블의 관계를 제약조건에 따라 구분할 수 있으며   
대표적으로 Oracle, MySQL, MriaDB, MS-SQL 등이 있습니다.

* * * 


2)  SQL    (Oracle)
  > 관계형 데이터베이서 관리 시스템 (RDBMS)의 데이터를 관리하기 위해 설계된 특수 목적의 프로그래밍 언어   


즉! 쉽게! 데이터를 관리하기위해 사용하는 언어입니다.
백번 설명보다 해보는게 최고입니다. 바로 사용법 보도록하죠
개념적으로   

> DDL_Data Definition Language (데이터 정의어)   

테이블 자체를 생성,변경,삭제 등

![ex_screenshot](./assets/built/images/ddl.png){: width="800" height="200}{: .center}



> DML_Data Manipulation Language (데이터 조작어)

테이블안의 내용을 조회,삽입,삭제 등 
![ex_screenshot](./assets/built/images/dml.png){: width="800" height="200}


> DCL_Data Control Language (데이터 제어어)

DB에 접근하고 객체를 사용함에 대한 권한에 대한 명령어
![ex_screenshot](./assets/built/images/dcl.png){: width="800" height="200}





> TCL_Transaction Control Language (트랜잭션 제어어)

논리적인 작업의 단위를 묶어서 DML 에 의한 조작된 결과를 작업단위(트랜잭션)별로 제어하는 명령어   
 :> 그냥 아차! 싶은 작업을 되돌릴수도 있고, 아차! 하기전에 저장하기도 할 수 있는 명령어      
![ex_screenshot](./assets/built/images/tcl.png){: width="800" height="200}



* * *





 
