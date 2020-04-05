---
title: "[Algorithms] Move Zeros"
layout: post
date: 2020-04-05 22:10
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---

https://leetcode.com/problems/move-zeroes/

~~~java
class Solution {
    public void moveZeroes(int[] nums) {
        Queue<Integer> zeros = new LinkedList<>();
        for(int i = 0; i < nums.length;i++){
            if(nums[i] == 0){
                zeros.add(i);
            }else{
                if(zeros.peek() != null){
                    nums[zeros.poll()] = nums[i];
                    nums[i] = 0;
                    zeros.add(i);
                }
            }
        }
    }
}
~~~

~~~java
class Solution {
    public void moveZeroes(int[] nums) {
        int nonZero = 0;
        for(int num : nums){
            if(num != 0 ){
                nums[nonZero] = num;
                nonZero++;
            }  
        }
        while(nonZero < nums.length){
            nums[nonZero] = 0;
            nonZero++;
        }
    }
}
~~~

