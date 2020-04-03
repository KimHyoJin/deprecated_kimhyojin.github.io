---
title: "[Algorithms] Happy number"
layout: post
date: 2020-04-03 23:00
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---

https://leetcode.com/explore/other/card/30-day-leetcoding-challenge/528/week-1/3284/

~~~java
class Solution {
    public boolean isHappy(int n) {
        int currentN = n;
        List<Integer> tempResult = new ArrayList<>();
        
        while(true){
            int temp = getDigitsSquareNumber(currentN);            
            if(temp == 1){
                return true;
            }else if(tempResult.contains(temp)){
                return false;
            }
            currentN = temp;
            tempResult.add(temp);
        }
    }
    
    private Integer getDigitsSquareNumber(int num){
        int result = 0;
        while (num > 0) {
            result = result + (num % 10) * (num % 10);
            num = num / 10;
        }
        return result;
    }
}
~~~

