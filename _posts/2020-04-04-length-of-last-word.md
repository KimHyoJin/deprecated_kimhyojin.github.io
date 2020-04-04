---
title: "[Algorithms] Length of Last Word"
layout: post
date: 2020-04-04 23:00
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---

https://leetcode.com/problems/length-of-last-word

~~~java
class Solution {
    public int lengthOfLastWord(String s) {
        int length = 0;
        for(int i = s.length()-1; i >= 0; i--){
            if(length == 0 && s.charAt(i) == ' '){
                continue;
            }    
            if(s.charAt(i) == ' '){
                return length;
            }
            length++;
        }
        return length;
    }
}
~~~

