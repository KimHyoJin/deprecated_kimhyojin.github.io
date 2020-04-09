---
title: "[Algorithms] Backspace string compare"
layout: post
date: 2020-04-09 23:53
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---



https://leetcode.com/problems/backspace-string-compare/

~~~java
class Solution {
    public boolean backspaceCompare(String S, String T) {
        return get(S).equals(get(T));
    }
    
    private String get(String s){
        Stack<Character> stack = new Stack<>();
        for(char temp : s.toCharArray()){
            if(temp == '#'){
                if(!stack.empty()){
                    stack.pop();
                }
            }else{
                stack.push(temp);
            }
        }
        String result = "";
        while(!stack.empty()){
            result = result + stack.pop();
        }
        return result;
    }
}
~~~

