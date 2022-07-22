---
layout: post
title: [코딩테스트] 오픈채팅방
author: qzce
description: 
categories: 
        - 코딩테스트
tags: 
        - 코딩테스트
        - 프로그래머스
date: '2021-06-02 09:00:00 +0900'
---

[문제링크](https://programmers.co.kr/learn/courses/30/lessons/42888)


```java
import java.util.*;

public String[] solution(String[] record) {
	String[] answer = {};
	
	HashMap<String, String> userArr = new HashMap<String, String>();
	
	for(int i=0; i<record.length; i++) {
		User user = new User();
		
		String[] temp = record[i].split(" ");
		
		if(!temp[0].equals("Leave")) {
			user.setUid(temp[1]);
			user.setName(temp[2]);
			
			userArr.put(user.getUid(), user.getName());
		}
		
	}
		
	List<String> answerList = new ArrayList<String>(); 
	
	for(int i=0; i<record.length; i++) {
		
		String[] temp = record[i].split(" ");
		
		if("Change".equals(temp[0])) {
			continue;
		}
		
		for(String key : userArr.keySet()) {
			
			if(temp[1].equals(key)){
				String ts = "";
				ts = userArr.get(key) + "님이 ";
				if("Enter".equals(temp[0])) {
					ts += "들어왔습니다.";
				} else if("Leave".equals(temp[0])) {
					ts += "나갔습니다.";
				}
				answerList.add(ts);
			}
		}
	}
	
	int arrListSize = answerList.size();        
	answer = answerList.toArray(new String[arrListSize]);
	
	return answer;
}

// 유저 정보
class User {
	
	private String uid;
	private String name;
	
	public String getUid() {
		return uid;
	}
	public void setUid(String uid) {
		this.uid = uid;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	
}
```
---
1. Map을 이용해 uid가 중복이면 마지막 바꾼 이름으로 uid의 이름을 설정
2. Change 제외 후 Enter, Leave에서 문장 만들기
3. 배열에 넣기