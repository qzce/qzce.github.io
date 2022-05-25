---
layout: post
title: jpa repository 기능
author: qzce
description: 
categories: [spring]
tags: 
        - java
        - jpa
date: '2021-04-14 10:00:00 +0900'
---




|명칭|설명|비고|
|---|---|---|
|findAll()| 전체 검색 | select * from table
|findBy~()| 검색 | 
|findBy~Contanining| 조건 검색 | select * from table where ~~
|save()| 저장 | insert
|deleteBy~()| 조건 삭제 | delete from table where ~~


**~ = 검색컬럼명**


