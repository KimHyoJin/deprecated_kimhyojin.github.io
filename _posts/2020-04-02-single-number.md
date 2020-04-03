---
title: "[Algorithms] single number"
layout: post
date: 2020-04-02 23:28
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---

https://leetcode.com/problems/single-number/

~~~java
class Solution {
    public int singleNumber(int[] nums) {
        Arrays.sort(nums);
        
        for(int num : nums){
            System.out.println("num: " + num);   
        }
        
        Integer temp = null;
        boolean hasTwo = false;
        for(int num : nums){
            System.out.println("num: " + num + " hasTwo: "+ hasTwo + " temp: "+ temp);   

            if(temp != null){
                if(!hasTwo && temp != num){
                    return temp;
                }
                hasTwo = (num == temp);
            }
            temp = num;
        }
        return nums[nums.length-1];

    }
}
~~~

