---
layout: post
title: 소수찾기
author: qzce
description: 
categories: 
        - 코딩테스트
tags: 
        - 코딩테스트
        - 프로그래머스
date: '2021-05-08 09:00:00 +0900'
---

[문제링크](https://programmers.co.kr/learn/courses/30/lessons/42839)


```java
import java.util.*;

public class alg3 {
	
	public static void main(String[] args) {

		solution("131");

	}

	public static int solution(String numbers) {

		String[] numberArr = numbers.split("");
		int[] arr = new int[numberArr.length]; 
		Set<Integer> resultSet = new HashSet<Integer>();
		ArrayList<Integer> resultList = new ArrayList<Integer>();
		
		for(int i=0; i<arr.length; i++) {
			arr[i] = Integer.valueOf(numberArr[i]);
		}
		
		for(int i=1; i<=arr.length; i++) {
			
			Permutation perm = new Permutation(arr.length, i); 
			perm.permutation(arr, 0); 
			Set<Integer> result = perm.getRes();
			Iterator<Integer> it = result.iterator();
			
			ArrayList<Integer> list = new ArrayList<Integer>();
			
			while (it.hasNext()) {
				list.add(it.next());
			}
			
			Collections.sort(list);
			
			for(int n : list) {
				ArrayList<Integer> pList = new ArrayList<Integer>();
				Pnumber pn = new Pnumber(n);
				pList = pn.makePnumber();
				for(int j : pList) {
					resultSet.add(j);
				}
			}
		}
		
		Iterator<Integer> it = resultSet.iterator();
		
		while(it.hasNext()) {
			resultList.add(it.next());
		}
		
		Collections.sort(resultList);
		
		System.out.println(resultList.toString());
		
		
		int answer = 0;
		return answer;
	}

}

// 소수 찾기
class Pnumber {
	private int n;
	private ArrayList<Integer> result;
	
	public Pnumber(int n) {
		this.n = n;
		this.result = new ArrayList<Integer>();
	}
	
	// 짝수 제외
	public ArrayList<Integer> makePnumber() {
		
		boolean[] bool = new boolean[n+1];
		
		Arrays.fill(bool, true);
		
		bool[0] = false;
		if(n>=1) { bool[1] = false; }
		
		for(int i=2; i*i<=n; i++) {
			if(bool[i]) {
				for(int j=i*i; j<=n; j+=i) {
					bool[j] = false;
				}
			}
		}
		
		for(int i=0; i<=n; i++) {
			if(bool[i]==true) {
				result.add(i);
			}
		}
		return result;
		
	}
}

// 순열
class Permutation { 
	
	private int n; 
	private int r; 
	private int[] now; 
	private Set<Integer> res; 
	
	public Set<Integer> getRes() { 
		return res; 
	} 
	
	public Permutation(int n, int r) { 
		this.n = n; 
		this.r = r; 
		this.now = new int[r]; 
		this.res = new HashSet<Integer>(); 
	} 
	
	public void swap(int[] arr, int i, int j) { 
		int temp = arr[i]; 
		arr[i] = arr[j]; 
		arr[j] = temp; 
	} 
	
	public void permutation(int[] arr, int depth) { 
		
		if (depth == r) { 
			ArrayList<Integer> temp = new ArrayList<>(); 
			
			for (int i = 0; i < now.length; i++) { 
				temp.add(now[i]);
			} 
			
			StringBuilder sb = new StringBuilder();
			
			for(int i=0; i<temp.size(); i++) {
				sb.append(temp.get(i));
			}
			res.add(Integer.valueOf(sb.toString()));
			
			return; 
		} 
		
		for (int i = depth; i < n; i++) { 
			swap(arr, i, depth); 
			now[depth] = arr[depth];
			permutation(arr, depth+1);
			swap(arr, i, depth); 
		} 
	
	}
}
```


### 에라토스테네스의 체
- n의 소수의 범위 : 2 <= (소수) < √n 
- 2~√n 까지의 숫자의 배수를 소거하는 식
- O(NlogN)

[나무위키](https://namu.wiki/w/%EC%97%90%EB%9D%BC%ED%86%A0%EC%8A%A4%ED%85%8C%EB%84%A4%EC%8A%A4%EC%9D%98%20%EC%B2%B4)

---
가장 큰 수를 찾아 그것의 소수만 찾으면 됨
