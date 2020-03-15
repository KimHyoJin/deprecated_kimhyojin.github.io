---
title: "[Algorithms] Longest Substring without Repeating Characters"
layout: post
date: 2020-02-15 21:36
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
description: LeetCode 알고리즘 문제풀기
---



## Problems

~~~java
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
~~~



## Solutions

~~~java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int index = 0;
        int maxLength = 0;
        while(index != s.length()){
            int length = getSubstring(s.substring(index));
            if(length > maxLength){
                maxLength = length;
            }
            index++;
        }
        return maxLength;
    }
    
    
    private int getSubstring(String s){
        Set<Character> duplicateChecker = new HashSet<>();
        for(int i = 0; i< s.length(); i++){
           char ch = s.charAt(i);
           if(duplicateChecker.contains(ch)){
               return i;
           }
           duplicateChecker.add(ch);
       }
        return s.length();
    }
}
~~~

그다지 좋은 solution은 아니고, discussion에 다음의 solution이 있었다. 

https://leetcode.com/problems/longest-substring-without-repeating-characters/discuss/1729/11-line-simple-Java-solution-O(n)-with-explanation