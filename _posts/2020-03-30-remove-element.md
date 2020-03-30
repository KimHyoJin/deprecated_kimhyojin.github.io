---
title: "[Algorithms] remove element"
layout: post
date: 2020-03-30 20:46
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---

https://leetcode.com/problems/remove-element/

~~~java
class Solution {
    public int removeElement(int[] nums, int val) {
        int index = 0;
        for(int i = 0; i< nums.length; i++){
            if(nums[i] != val){
                nums[index] = nums[i];
                index++;
            }
        }
        return index;
    }
}
~~~

