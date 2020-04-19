---
title: "[Algorithms] Maximum depth of binary tree"
layout: post
date: 2020-04-16 23:33
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---

https://leetcode.com/problems/maximum-depth-of-binary-tree/submissions/

~~~java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int maxDepth(TreeNode root) {
        return maxDepth(root, 0);
    }
    
    public int maxDepth(TreeNode node, int depth){
        if(node == null)
            return depth;
        
        depth++;
        return Math.max(maxDepth(node.left, depth), maxDepth(node.right, depth));
    }
}
~~~

