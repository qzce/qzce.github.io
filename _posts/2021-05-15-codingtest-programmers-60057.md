---
layout: post
title: [코딩테스트] 문자열 압축
author: qzce
description: 
categories: 
        - 코딩테스트
tags: 
        - 코딩테스트
        - 프로그래머스
date: '2021-05-15 09:00:00 +0900'
---

[문제링크](https://programmers.co.kr/learn/courses/30/lessons/60057)


```java
import java.util.*;

public class StringCompression {

	public static void main(String[] args) {

		solution("xababcdcdababcdcd");
	}
	
	public static int solution(String s) {
		
		int answer = 0;
		
		ArrayList<Integer> list = new ArrayList<Integer>();
		
		CutLength cl = new CutLength(s);
		list = cl.cutLength();
		
		answer = Collections.min(list);
		
		System.out.println(answer);
		
        return answer;
    }

}

// 문자열 자르기
class CutLength {
	
	private String s;
	
	public CutLength(String s) {
		this.s = s;
	}
	
	public ArrayList<Integer> cutLength() {
		
		ArrayList<Integer> result = new ArrayList<Integer>();
		
		for(int i=0; i<s.length()/2; i++) {
			
			ArrayList<String> list = new ArrayList<String>();
			
			for(int j=0; j<s.length()-i; j+=i+1) {
				list.add(s.substring(j, j+(i+1)));
				
				if(s.length()-i <= j+(i+1) && j+(i+1) != s.length()) {
					list.add(s.substring(s.length()-i+1, s.length()));
				}
			}
			
			ListValue listValue = new ListValue(list, i+1);
			result.add(listValue.listValue());
		}
		
		return result;
		
	}
	
}

// 전체 리스트 출력
class ListValue {
	
	private ArrayList<String> list;
	private int size;
	
	public ListValue(ArrayList<String> list, int size) {
		this.list = list;
		this.size = size;
	}
	
	public int listValue() {
		
		System.out.println(list.toString());
		
		int returnVal = 0;
		
		StringBuilder sb = new StringBuilder();
		
		for(int i=0; i<list.size(); i++) {
			int t = 0;
			String ts = list.get(i); 
			for(int j=i+1; j<list.size(); j++) {
				if(list.get(i).equals(list.get(j))) {
					t++;
				} else {
					break;
				}
			}
			i = i+t;
			
			if(t!=0) {
				ts = t+1+ts;
			}
			sb.append(ts);
		}
		System.out.println(sb.toString());
		return sb.toString().length();
		
	}
}
```

---
1. 문자열을 1~문자열사이즈까지 자른 모든 경우의 수 출력
2. 위 경우별로 변환시켜서 길이 비교해서 가장 작은 값