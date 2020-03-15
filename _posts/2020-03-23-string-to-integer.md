---
title: "[Algorithms] string to integer"
layout: post
date: 2020-03-23 21:22
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---

https://leetcode.com/problems/string-to-integer-atoi



~~~java
class Solution {
    
    private static final Set<Character> SIGN = Set.of('+','-');
        private static final Set<Character> NUMBER = Set.of('1','2','3','4','5','6','7','8','9','0');

    public int myAtoi(String str) {
        boolean isPositive = true;
        String tempStr = str;
        
        do{
            tempStr = tempStr.replaceFirst(" ", "");
            if(tempStr.equals("")){
                return 0;
            }
        }while(tempStr.charAt(0) == ' ');
        
        if(tempStr.charAt(0) == '-'){
            isPositive = false;
        }

            
        try{   
            if(NUMBER.contains(tempStr.charAt(0)) || (SIGN.contains(tempStr.charAt(0)) && NUMBER.contains(tempStr.charAt(1)))){
                if(SIGN.contains(tempStr.charAt(0))){
                    tempStr = tempStr.substring(1,tempStr.length());
                }
                tempStr = tempStr.replaceAll("[a-zA-Z-.+ ][0-9]*", ""); 
            }else{
                return 0;
            }
            return isPositive ? Integer.valueOf(tempStr) : Integer.valueOf(tempStr) * (-1);

        }catch(NumberFormatException e){
            return isPositive ? Integer.MAX_VALUE : Integer.MIN_VALUE;
        }catch(Exception e){
            return 0;
        }
    }
}
~~~

