---
title: "[Algorithms] Duplicate Emails"
layout: post
date: 2020-04-19 23:33
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---





https://leetcode.com/problems/duplicate-emails/

~~~mysql
SELECT Email FROM 
(SELECT Email, COUNT(Email) AS Count FROM Person GROUP BY Email) sub 
WHERE Count > 1 
~~~

위 방법은 내가 사용한 subquery를 이용한 방법. Discussion에서는 Having을 사용한 방법이 나와 있었다.

~~~mysql
SELECT Email FROM Person GROUP BY Email HAVING COUNT(*) > 1
~~~

