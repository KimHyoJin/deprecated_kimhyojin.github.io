---
title: "[Algorithms] valid parentheses"
layout: post
date: 2020-03-24 18:33
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---

https://leetcode.com/problems/valid-parentheses

~~~java
class Solution {
    
    private static final List<Character> OPEN = List.of('(','[','{');
    private static final List<Character> CLOSE = List.of(')',']','}');
    
    public boolean isValid(String s) {
        
        Stack<Character> stack = new Stack<>();
        int i = 0;
        
        while(i < s.length()){
            Character temp = s.charAt(i);
            if(OPEN.contains(temp)){
                stack.push(temp);
            }else{
                if(stack.empty() || OPEN.indexOf(stack.pop()) != CLOSE.indexOf(temp)){
                    return false;
                }
            }
            i++;
        }
        return stack.empty();
    }
}
~~~

