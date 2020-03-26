---
title: "[Algorithms] remove duplicates from sorted array"
layout: post
date: 2020-03-25 18:33
image: 
headerImage: false
tag: algorithm
category: blog
author: 효징
hidden: false
description: LeetCode Algorithm 문제 풀기
---

https://leetcode.com/problems/remove-duplicates-from-sorted-array/

~~~java
class Solution {
    public int removeDuplicates(int[] nums) {
        int index = 0;
        int flag = 0;
        for (int i = 0; i < nums.length; i++) {
            flag = 0;
            for (int j = 0; j < index; j++) {
                if (nums[i] == nums[j]) {
                    flag = 1;
                }
            }
            if (flag == 0) {
                nums[index] = nums[i];
                index++;
            }
        }
        return index;
    }
}
~~~



이번 문제는 약간 고민이 필요했다. 처음에 구현은 다음처럼 했다

~~~java
public static int removeDuplicates(int[] nums) {
		nums = Arrays.stream(nums).distinct().toArray();
}
~~~

위처럼 구현하면 될줄 알았다. 그러나 결과적으로 `nums` 는 변경되지 않았다. 

이는 call-by-value, call-by-reference와 관계있다.



## Call-By-Value vs Call-By-Reference

Call by value 와 call by reference를 두고 의미만 생각해보면, 한쪽은 value(값)값을 전달하고 다른쪽은 reference(참조값)을 전달하는 것이다. 이해하기 조금 어렵다면 이렇게 부연설명을 붙이는 것이 이해하기 편리하다

call by value : 메모리 할당 시 **값**을 pointing
call by reference : 메모리 할당 시 값이 담긴 **주소값**을 pointing

Java는 기본적으로 call by value이다. 아무래도 내가 겪었던 문제를 풀어서 정리하는게 도움이 될것 같아 풀어서 적어보겠다!



### 실패한 코드 

내가 처음에 생각했던 코드를 다시 살펴보자. 

~~~java
public static int removeDuplicates(int[] nums) {
		nums = Arrays.stream(nums).distinct().toArray();
}
~~~

테스트 코드는 다음과 같다

```java
public static void main(String[] args) {
    int[] test = {1, 1, 2};
    int len = removeDuplicates(test);

    for (int i = 0; i < len; i++) {
        System.out.println(test[i]);
    }
}
```

변수들이 어떻게 할당되고 어떤 값을 가지고 있는지는 아래를 살펴보자

```java
Variable																		Address			Value
test																				0x00000			{1,1,2}
```

`removeDuplicates` 를 실행하면 다음과 같이 된다

~~~java
Variable																		Address			Value
test																				0x00000			{1,1,2}
nums																				0x00000			{1,1,2}
~~~

Call by value이므로 nums는 test의 값을 바라보게 된다.  (같은 주소의 메모리를 할당받은 것이 아닌 nums가 어디를 바라보고 있는지를 표시하기 위해 위처럼  표기하였다)

`nums = Arrays.stream(nums).distinct().toArray();` 이 코드를 실행하면

~~~java
Variable																		Address			Value
test																				0x00000			{1,1,2}
Arrays.stream(nums).distinct().toArray()		0x00001			{1,2}
nums																				0x00001			{1,2}
~~~

그러나 `Arrays.stream(nums).distinct().toArray();` 는 새로 `0x00001` 에 할당되게 되고 nums는 이를 바라보게 된다. 결국 test의 값은 변경되지 않는다. 따라서 해결되지 않는 것이다.



### 성공한 코드

그렇다면 테스트를 성공한 코드는 어떻게 변경되게 된걸까?

~~~java
public int removeDuplicates(int[] nums) {
		int index = 0;
    int flag = 0;
    for (int i = 0; i < nums.length; i++) {
    		flag = 0;
      	for (int j = 0; j < index; j++) {
      			if (nums[i] == nums[j]) {
            		flag = 1;
            }
        }
        if (flag == 0) {
            nums[index] = nums[i];
            index++;
        }
		}
		return index;
}
~~~

마찬가지로 처음은 이런 상태이다

```java
Variable			Address			Value
test					0x00000			{1,1,2}
```

`removeDuplicates` 를 실행하면 다음과 같이 된다

~~~java
Variable			Address			Value
test					0x00000			{1,1,2}
nums					0x00000			{1,1,2}
~~~

nums에 변경이 일어나므로 nums가 가르키고 있는 address `0x00001` 의 값에 변화가 일어난다. (마찬가지로 같은 주소의 메모리를 할당받은 것이 아닌 nums가 어디를 바라보고 있는지를 표시하기 위해 위처럼  표기하였다)

~~~java
Variable			Address			Value
test					0x00000			{1,2}
nums					0x00000			{1,2}
~~~

따라서 이 경우 변경되게 되는 것이다. 

### 만약 call by reference 라면?

만약 java가 call by reference라면 다음의 코드는 이렇게 실행되어야 한다

~~~java
public static int removeDuplicates(int[] nums) {
		nums = Arrays.stream(nums).distinct().toArray();
}
~~~

처음은 다음과 같다.

~~~java 
Variable																		Address			Value
test																				0x00000			{1,1,2}
nums																				0x00000			{1,1,2}
~~~

`nums` 는 `test` 의 주소값을 바라보게 된다. `nums` 에 `Arrays.stream(nums).distinct().toArray();` 를 넣게 되므로 `nums` 가 가르키는 주소의 value는 `Arrays.stream(nums).distinct().toArray();` 의 결과로 변경되게 된다. 따라서 다음과 같아진다

~~~java
Variable																		Address			Value
test																				0x00000			{1,2}
nums																				0x00000			{1,2}
~~~

따라서 call by reference인 경우 실패한 코드도 문제 없이 동작하여야 한다. 



## Other Solution

Disscussion의 솔루션은 다음과 같다

~~~java
public int removeDuplicates(int[] nums) {
    int i = nums.length > 0 ? 1 : 0;
    for (int n : nums)
        if (n > nums[i-1])
            nums[i++] = n;
    return i;
}
~~~

sorted array라는 조건이 있어 이를 활용한 모습이당.. 문제를 제대로 읽어야겠네

~~~
Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
~~~





##### reference

https://stackoverflow.com/questions/40480/is-java-pass-by-reference-or-pass-by-value

https://sleepyeyes.tistory.com/11

