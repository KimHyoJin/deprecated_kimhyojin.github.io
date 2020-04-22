---
title: "[Algorithms] Fibonacci number"
layout: post
date: 2020-04-22 23:35
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---

https://leetcode.com/problems/fibonacci-number/submissions/

~~~java
class Solution {
    public int fib(int N) {
        if(N == 1){
            return 1;
        }else if(N == 0){
            return 0;
        }
        return fib(N-1) + fib(N-2);
    }
}
~~~