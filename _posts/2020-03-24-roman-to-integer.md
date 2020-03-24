---
title: "[Algorithms] roman to integer"
layout: post
date: 2020-03-24 18:44
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---

https://leetcode.com/problems/roman-to-integer/

~~~java
class Solution {
    Map<Character, Integer> RULE = Map.of('I', 1, 'V', 5, 'X', 10, 'L', 50, 'C', 100, 'D', 500, 'M', 1000);

    public int romanToInt(String s) {
        int i = 0;
        Integer previous = null;
        int total = 0;
        while (i < s.length()) {
            Integer temp = RULE.get(s.charAt(i));
            if (previous != null && temp > previous) {
                total = total - previous + temp - previous;
            } else {
                total = total + temp;
            }
            previous = temp;
            i++;
        }
        return total;
    }
}
~~~

