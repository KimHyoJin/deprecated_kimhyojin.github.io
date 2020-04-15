---
title: "[Algorithms] Remove duplicates from sorted list"
layout: post
date: 2020-04-15 23:33
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---



https://leetcode.com/problems/remove-duplicates-from-sorted-list

~~~java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null){
            return null;
        }
        
        int tempVal = head.val;
        ListNode temp = head;
        ListNode tempBefore = head;
        
        while(temp != null){
            if(tempVal != temp.val){
                tempVal = temp.val;
                tempBefore.next = temp;
                tempBefore = temp;
            }
            temp = temp.next;
        }
        tempBefore.next = null;
        return head;
    }
}
~~~

