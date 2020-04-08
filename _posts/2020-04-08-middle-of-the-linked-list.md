---
title: "[Algorithms] middle of the linked list"
layout: post
date: 2020-04-08 19:31
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---

https://leetcode.com/problems/middle-of-the-linked-list

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
    public ListNode middleNode(ListNode head) {
        ListNode temp = head;
        int length = 0;
        while(temp != null){
            length++;
            temp = temp.next;
        }
        System.out.println("find");
        temp = head;
        int index = 0;
        while(index < length / 2){
            temp = temp.next;
            index++;
        }
        return temp;
    }
}
~~~



하나는 두칸씩 가고, 하나는 한칸씩 간다. 

~~~java
public ListNode middleNode(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
~~~

