---
layout: post
title: [코딩테스트] 거리두기 확인하기
author: qzce
description: 
categories: 
        - 코딩테스트
tags: 
        - 코딩테스트
        - 프로그래머스
date: '2021-07-14 09:00:00 +0900'
---

[문제링크](https://school.programmers.co.kr/learn/courses/30/lessons/81302)


```java
import java.util.*;

class Solution2 { 
	
	private Candidate caOne = new Candidate(-1, -1);
	
    public int[] solution(String[][] places) {
    	
        int[] answer = new int[places.length];
        
        for(int i=0; i<places.length; i++) {
    		
    		boolean chk = true;
    		
	        for(int j=0; j<places[i].length; j++) {
	        	
	        	if(!chk) {
	        		break;
	        	}
	        	
	        	String[] line = places[i][j].split("");
	        	
	        	for(int k=0; k<line.length; k++) {
	        		
	        		if("P".equals(line[k])) {
	        			Candidate ca = new Candidate(j, k); 
	        			if(distance(places[i], ca, true)) {	// true : 안맞음
	        				chk = false;
	        				break;
	        			}
	        		}
	        	}
	        }
	        
	        if(chk) {
	        	answer[i] = 1;
	        } else {
	        	answer[i] = 0;
	        }
	        
        }
    	
    	for(int i : answer) {
    		System.out.println(i);
    	}
    	
        return answer;
    }
    
    public boolean distance(String[] places, Candidate ca, boolean seq) {
    	
    	int[] dx = {-1,1,0,0};
    	int[] dy = {0,0,1,-1};
    	
    	boolean returnVal = false;
    	
		for(int j=0; j<dx.length; j++) {
			
			int nx = ca.getX() + dx[j];
			int ny = ca.getY() + dy[j];
			
			if(nx < 0 || ny < 0 || nx > 4 || ny > 4 || (caOne.getX() == nx && caOne.getY() == ny)) {
				continue;
			}
			
			if('P' == places[nx].charAt(ny)) {
				// 끝
				return true;
			} else if('X' == places[nx].charAt(ny)) {
				// 다른 방향 찾기
			} else if('O' == places[nx].charAt(ny)) {
				// 그 방향에서 더 찾기
				if(seq) {
					Candidate ca2 = new Candidate(nx, ny);
					caOne = ca;
					if(distance(places, ca2, false)) {
						returnVal = true;
					}
				}
			}
			
		}
		return returnVal;
    }
}

// 응시자
class Candidate {
	
	private int x;
	private int y;
	
	public Candidate(int x, int y) {
		this.x = x;
		this.y = y;
	}

	public int getX() {
		return x;
	}

	public void setX(int x) {
		this.x = x;
	}

	public int getY() {
		return y;
	}

	public void setY(int y) {
		this.y = y;
	}
	
	
}
```





#### 알고리즘

###### 예시 대기실

|       | 0    | 1    | 2    | 3    | 4    |
| ----- | ---- | ---- | ---- | ---- | ---- |
| **0** | P    | O    | O    | P    | X    |
| **1** | O    | X    | O    | X    | P    |
| **2** | P    | X    | P    | X    | O    |
| **3** | O    | X    | X    | X    | O    |
| **4** | O    | O    | O    | P    | P    |

##### (2.2) P 기준

|       | 0    | 1    | 2    | 3    | 4    |
| ----- | ---- | ---- | ---- | ---- | ---- |
| **0** |      |      | O    |      |      |
| **1** |      | X    | O    | X    |      |
| **2** | P    | X    | P    | X    | O    |
| **3** |      | X    | X    | X    |      |
| **4** |      |      | O    |      |      |

1. 맨해튼 거리(2)인 다이아몬드 모양으로 체크할 수 있음

2. 사방으로 하나씩 1씩 움직여서

- X를 만나면 : 어디에 P가 있던 상관없음 > 안봐도됨

- P를 만나면 : 맨해튼 거리에 포함되니 해당 대기실에 대해서 0을 반환 하고 끝냄

- O를 만나면 : 해당 자리에 대해서 위 조건을 다시 체크

