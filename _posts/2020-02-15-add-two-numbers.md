---
title: "[Algorithms] Add Two Numbers"
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
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
~~~



## Solutions

~~~java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        add(null, l1, l2, 0);
        return l1;
    }
    
    
    public ListNode add(ListNode prev, ListNode l1, ListNode l2, int over){
        if( l1 == null && l2 == null && over == 0){
            return null;
        }
        
        int total =  getVal(l1) + getVal(l2) + over;
        over = total / 10;
        
        if(l1 == null){
            prev.next = new ListNode(total % 10);
            l1 = prev.next;
        }else{
           l1.val = total % 10;         
        }
     
        return add(l1, getNext(l1), getNext(l2), over);
    }
    
    private ListNode getNext(ListNode node){
        if(node == null){
            return null;
        }
        return node.next;
    }
    
    
    private int getVal(ListNode node){
        if(node == null){
            return 0;
        }
        return node.val;
    }
} 
~~~

 ```getNext```나 ```getVal```의 경우는 ```Optional```로 변경하여 구현가능할 것같은데, leetcode에서 테스트는 못해봤다 (Optional 지원이 안되는듯?)