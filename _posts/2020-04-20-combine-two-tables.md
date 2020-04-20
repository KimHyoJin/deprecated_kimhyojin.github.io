---
title: "[Algorithms] Combine Two Tables"
layout: post
date: 2020-04-20 22:35
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---

https://leetcode.com/problems/combine-two-tables/submissions/

~~~mysql
# Write your MySQL query statement below
SELECT person.FirstName, person.LastName, address.City, address.State
FROM Person person LEFT OUTER JOIN Address address ON address.PersonId = person.PersonId;
~~~

