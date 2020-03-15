---
title: "bash script cheat sheet - for loop (1)"
layout: post
date: 2019-07-20 11:52
image: 
headerImage: false
tag: bash
category: blog
author: 효징
description: bash script 시리즈를 연재해보려고 합니다. 그 첫번째 for-loop
---
Bash script를 짜는 경우가 대학원을 그만 둔 뒤에는 거의 없는 데 … 그래서인지 가끔씩 script를 짜야할 때 다 까먹어서 찾아보느라 시간이 걸리곤 한다. 그런 의미로 이곳에 bash의 기본적인 내용을 하나하나씩 적어보려고 합니다. 많은 예제는 아마도 Gist로 짧게 올릴듯 싶습니다!

Gist : https://gist.github.com/KimHyoJin 심심하면 들어오세용

## for loop

기본적으로 for loop는 다음의 형태입니다

~~~bash
#!/bin/bash

for i in <range>
do
	<do something>
done
~~~



for문을 짤때는 아무래도 저 위의 스크립트에서 <range> 이 부분을 어떻게 줄것인가가 가장 어려운 부분입니다

### sequence

순차적으로 증가하는 경우는 다음처럼 쓸 수 있습니다

#### use seq

~~~bash
for i in $(seq 0 10)
do
        echo $i
done
~~~

여기서 start, end는 모두 inclusive다. 

#### use range

~~~bash
for i in {0..10}
do
        echo $i
done
~~~

이 또한 start, end는 모두 inclusive다. 

#### use variable

~~~bash
for ((i=0;i<11;i++))
do
        echo $i
done
~~~

 C와 가장 유사한 방법



### Non-sequence

연속적인 수의 범위에서가 아닐 때의 for loop 돌리는 방법

#### write all elememt

~~~bash
for i in 0 2 4 6 8 10
do
        echo $i
done
~~~



#### use seq

~~~bash
for i in $(seq 0 2 10)
do
        echo $i
done
~~~

~~~bash
seq <start> <increment> <end>
~~~



#### use range

~~~bash
for i in {0..10..2}
do
        echo $i
done
~~~

위의 예제는 bash 4.0 이상에서만 동작한다고 한다.. 나는 3.2라 테스트를 못해봄 (버전업은 조금 귀찮았다..)



#### use variable

~~~bash
for ((i=0;i<11;i=i+2))
do
				echo $i
done
~~~



### 이런것도 됩니다!

#### padding 두기

~~~bash
for i in $(seq -f "%02g" 0 2 10)
do
        echo $i
done
~~~

여기서 f는 format의 약자인데 일반 print와는 다르게 %02d로는 동작하지 않습니다. %02g라고 쳐야합니다.

혹은 seq에 -w 옵션을 줘도 됩니다. 여기서 w는 width의 약자이며 equal-width, 즉 최대 숫자와 같은 길이를 줍니다. (참고 : https://linux.die.net/man/1/seq)

~~~bash
for i in $(seq -w 0 2 10)
do
        echo $i
done
~~~

 

bash 4.0 이상에서는 range를 이용해서도 padding이 가능하다고 한다. 테스트는 못해보았습니다. 

~~~bash
for i in {01..10}
do
        echo $i
done
~~~



혹은 가장 간단한 방법으로 출력시 padding을 줄 수도 있습니다

~~~bash
for i in {1..10}
do
        printf "%02d\n" $i
done
~~~



To be continue …
