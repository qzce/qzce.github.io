layout: post
title: [코딩테스트] 괄호변환
author: qzce
description: 
categories: 

   - 코딩테스트
     tags: 
        - 코딩테스트
          그래머스
          date: '2021-07-22 09:00:00 +0900'

---

[문제링크](https://programmers.co.kr/learn/courses/30/lessons/60058)


```java
class Solution {
    
    public String solution(String p) {
        String answer = "";
        
        answer += divideStr(p);
        
        return answer;
    }
    
    public String divideStr(String p) {
        
        if("".equals(p)) {
            return "";
        }
        
        String returnVal = "";
        
        ArrayList<String> u = new ArrayList<String>();
        ArrayList<String> v = new ArrayList<String>();
        
        int leftBracket = 0;
        int rightBracket = 0;
        boolean uvChk = true;
        boolean properChk = true;
        
        String[] pArr = new String[p.length()];
        pArr = p.split("");
        
        for(int i=0; i<pArr.length; i++) {
             if(pArr[i].equals("(")) {
                 leftBracket++;
             } else if(pArr[i].equals(")")) {
                 rightBracket++;
             }
             
             if(uvChk) {
                 u.add(pArr[i]);
                 if(leftBracket-rightBracket < 0) {
                     properChk = false;
                 }
             }else {
                 v.add(pArr[i]);
             }
             
             if(leftBracket == rightBracket) {
                 uvChk = false;
             }
        }

        if(properChk) { // u는 올바름
            // v 실행 + u return
            returnVal += String.join("", u) + divideStr(String.join("", v));
        } else {
            // ( + v실행 + ) + u앞뒤 자르고 뒤집기
            returnVal += "(" + divideStr(String.join("", v)) + ")" + reverseBracket(u);
        }
        
        return returnVal;
    }
    
    public String reverseBracket(ArrayList<String> u) {
        String reverse = "";
        for(int i=1; i<u.size()-1; i++) {
            if("(".equals(u.get(i))) {
                reverse += ")";
            } else if(")".equals(u.get(i))) {
                reverse += "(";
            }
        }
        
        return reverse;
    }
    
}
```



```
1. 입력이 빈 문자열인 경우, 빈 문자열을 반환합니다. 
2. 문자열 w를 두 "균형잡힌 괄호 문자열" u, v로 분리합니다. 단, u는 "균형잡힌 괄호 문자열"로 더 이상 분리할 수 없어야 하며, v는 빈 문자열이 될 수 있습니다. 
3. 문자열 u가 "올바른 괄호 문자열" 이라면 문자열 v에 대해 1단계부터 다시 수행합니다. 
  3-1. 수행한 결과 문자열을 u에 이어 붙인 후 반환합니다. 
4. 문자열 u가 "올바른 괄호 문자열"이 아니라면 아래 과정을 수행합니다. 
  4-1. 빈 문자열에 첫 번째 문자로 '('를 붙입니다. 
  4-2. 문자열 v에 대해 1단계부터 재귀적으로 수행한 결과 문자열을 이어 붙입니다. 
  4-3. ')'를 다시 붙입니다. 
  4-4. u의 첫 번째와 마지막 문자를 제거하고, 나머지 문자열의 괄호 방향을 뒤집어서 뒤에 붙입니다. 
  4-5. 생성된 문자열을 반환합니다.
```



1. 입력이 빈 문자열인 경우, 빈 문자열을 반환합니다. 

```java
 public String divideStr(String p) {
        if("".equals(p)) {
            return "";
        }
        ...
}
```

2. 문자열 w를 두 "균형잡힌 괄호 문자열" u, v로 분리합니다. 단, u는 "균형잡힌 괄호 문자열"로 더 이상 분리할 수 없어야 하며, v는 빈 문자열이 될 수 있습니다. 

```java
	String[] pArr = new String[p.length()];
    pArr = p.split("");

    for(int i=0; i<pArr.length; i++) {
    
        if(pArr[i].equals("(")) {
            leftBracket++;
        } else if(pArr[i].equals(")")) {
            rightBracket++;
        }

        if(uvChk) {
            u.add(pArr[i]);
        if(leftBracket-rightBracket < 0) {
            properChk = false;
        }
        }else {
            v.add(pArr[i]);
        }

        if(leftBracket == rightBracket) {
            uvChk = false;
        }
	}
```

3. 문자열 u가 "올바른 괄호 문자열" 이라면 문자열 v에 대해 1단계부터 다시 수행합니다. 
   3-1. 수행한 결과 문자열을 u에 이어 붙인 후 반환합니다. 

```java
		if(properChk) { // u는 올바름
            // v 실행 + u return
            returnVal += String.join("", u) + divideStr(String.join("", v));
         }
```

4. 문자열 u가 "올바른 괄호 문자열"이 아니라면 아래 과정을 수행합니다. 
   4-1. 빈 문자열에 첫 번째 문자로 '('를 붙입니다. 
     4-2. 문자열 v에 대해 1단계부터 재귀적으로 수행한 결과 문자열을 이어 붙입니다. 
     4-3. ')'를 다시 붙입니다. 
     4-4. u의 첫 번째와 마지막 문자를 제거하고, 나머지 문자열의 괄호 방향을 뒤집어서 뒤에 붙입니다. 
     4-5. 생성된 문자열을 반환합니다.

```java
if(!properChk) {
	returnVal += "(" + divideStr(String.join("", v)) + ")" + reverseBracket(u);
}

	public String reverseBracket(ArrayList<String> u) {
        String reverse = "";
        for(int i=1; i<u.size()-1; i++) {
            if("(".equals(u.get(i))) {
                reverse += ")";
            } else if(")".equals(u.get(i))) {
                reverse += "(";
            }
        }
        
        return reverse;
    }
```

