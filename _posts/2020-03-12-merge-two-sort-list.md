---
title: "[Algorithms] Merge Two Sorted Lists"
layout: post
date: 2020-03-12 21:48
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---

https://leetcode.com/problems/merge-two-sorted-lists/

```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode pointer1 = l1;
        ListNode pointer2 = l2;
        ListNode start = new ListNode(0);
        ListNode result = start;
        
        while(true){
            printNode(result.next);
            if(pointer1 == null){
                start.next = pointer2;
                break;
            }else if(pointer2 == null){
                start.next = pointer1;
                break;
            }
            
            if(pointer1.val > pointer2.val){
                start.next = pointer2;
                pointer2 = pointer2.next;
            }else{
                start.next = pointer1;
                pointer1 = pointer1.next;
            }
            start = start.next;
        }
        
        return result.next;
    }
    
    private void printNode(ListNode node){
        while(node != null){
            System.out.print(node.val + "->");
            node = node.next;
        }
        System.out.print("\n");
    }
}
```

