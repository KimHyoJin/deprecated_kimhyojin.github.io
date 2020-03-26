---
title: "[Algorithms] maximum subarray"
layout: post
date: 2020-03-26 18:33
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---



https://leetcode.com/problems/maximum-subarray

~~~java
class Solution {
    public int maxSubArray(int[] nums) {
        int result = nums[0]; int end = nums[0];
        for(int i = 1; i < nums.length; i++){
            end = Math.max(end + nums[i], nums[i]);
            result = Math.max(end, result);
        }
        
        return result;
    }
}
~~~

