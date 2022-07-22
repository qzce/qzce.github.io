---
layout: post
title: [코딩테스트] 기능개발
author: qzce
description: 
categories: 
        - 코딩테스트
tags: 
        - 코딩테스트
        - 프로그래머스
date: '2021-07-04 09:00:00 +0900'
---

[문제링크](https://school.programmers.co.kr/learn/courses/30/lessons/42586)


```java
import java.util.ArrayList;

class Solution {
	
    public int[] solution(int[] progresses, int[] speeds) {
    	
    	ArrayList<Integer> arr = new ArrayList<Integer>();
		int order = 0, completeWork = 0;
		boolean addCheck = false;
		
        // 최대 100번 반복
		for(int i=0; i<100; i++) {
			completeWork = 0;	// 초기화
			addCheck = false;	
            
            // order 시작 이유 : 이미 지나간 작업은 불필요한 작업
			for(int j=order; j<progresses.length; j++) {
				progresses[j] += speeds[j];
                
                // 진도 100% 넘으면 배열에 넣기
				if(progresses[order] >= 100) {
					order++;
					completeWork++;
					addCheck = true;
				}
			}
            // 배열에 넣기
			if(addCheck) {
				arr.add(completeWork);
			}
            // 전체 작업 끝나면 종료
			if(progresses.length <= order) {
				break;
			}
		}
			
        // 답 제출
		int[] answer = new int[arr.size()];
		
		for(int i=0; i<arr.size(); i++) {
			answer[i] = arr.get(i);
		}
		
		return answer;
		
    }
}
```





#### 간단 알고리즘

1. 모든 작업에 각각 개발시간을 더함
2. 맨 앞 작업이 100을 넘는지 확인
3. 맨 앞 작업부터 100 이상 개수 구하여 배열에 넣음
4. 맨 앞을 3번에서 구한 개수로 바꿈
5. 모든 작업이 끝날때까지 1~4 반복