---
title: "[OneDay OneCommit] 1일 1커밋을 하면서"
layout: post
date: 2020-04-28 15:35
image: 
headerImage: false
tag: onedayonecommit
category: blog
author: 효징
hidden: false
description: Oneday Onecommit 회고 1
---

### 나의 1일 1커밋 History

![image-20200428154951018](/Users/kimhyojin/Library/Application Support/typora-user-images/image-20200428154951018.png)

1. TIL (Today I Learned)를 작성하면서 초록색으로 물든 Git public contribution을 자랑하는 수많은 글들을 보았었다. (이때까지만 해도 그렇게 큰 자극이 되지 않았다ㅎ)

2. 인턴 시절 멘토님께서 TIL을 작성하는것이 큰 도움이 된다고 하셨고 그래서 한달여간 작성을 했었는데 생각보다 나에게는 큰 부담이었다. 글을 못써서 그런걸까? 그렇게 흐지부지하다 그만두게 되었다
3. 회사 동료가 잔디밭 프로젝트(Git Public Contribution을 초록색으로 물들이는 프로젝트)를 한다고 알려주었다. 기회가 안되서 난 같이 못했지만 나도 해볼까 하는 생각이 들었다



나는 2번의 경험으로 뭔가 거창하게 시작하면 백퍼 중간에 그만둘거라는 감이 왔다. 그래서 정한 것은 알고리즘 문제풀기였다. 당시 알고리즘 문제에 약간 열올리고 있을 때였고, ''그냥 Git Gist처럼 정리를 하자'' 라는 마음으로 시작했다. 



### 너, 내 동료가 되라!

알고리즘 문제풀기로 1일 1커밋을 매우매우 가볍게 만들었지만, 그래도 혹시 안하지 않을까하는 마음에 함께할 친구들을 모집했다. 이직 준비를 하고 있는 S씨와 개인프로젝트를 함께 하고 있던 R씨보고 함께 하자고 했다. 규칙은 회사 동료가 참여하는 프로젝트의 규칙을 살짝 배껴왔다. 10만원을 미리 보증금으로 내고, 하루 빼먹을때마다 1천원씩 깎는 규칙이다. 

주기적으로 체크하기 위해 서로 1일 1커밋동안 한 일을 공유하는 시간도 갖기로 했다 (그래서 이 글을 쓴다)



### 1000원을 잃고 싶지 않아서 만든 토이 프로젝트 

문제는 1일 1커밋한 내용을 각자 github에 들어가서 확인해도 되지만, 친구들의 github까지 들어가서 보기가 너무 귀찮았다. 그리고 정산할때 이걸 언제 하나하나 세고 있나..? 그래서 github에 commit한 날짜를 한눈에 볼 수 있는 무엇인가를 토이프로젝트로 진행해보기로 했다. 

처음에는 카카오톡채널을 이용하여 매일매일 개발한 이력을 볼 수 있고, 기간동안의 commit한 날짜를 볼 수 있도록 개발하려고 했으나 메세지를 보내는 기능을 사용하려면 사업자 번호가 있어야 하기에, 간단한 웹사이트를 제작하기로 했다



#### Technical Stack

- Front End (React.js) 
- Gradle
- Spring boot 2
- Spring webflux
- Github API



#### How I Implementing

Github에서는 [Rest API](https://developer.github.com/v3/)를 제공해주고 있다. 이 중 내가 필요한 기능을 구현하려면, user별로 commit을 받아올 수는 없고 이런식으로 repo별로 commit을 받아올 수 가 있다. 이를 이용해서 개발을 하였다.

https://api.github.com/repos/KimHyoJin/kimhyojin.github.io/commits



##### 2020년 5월 초, 지금까지의 개발

![image-20200504202359244](/Users/kimhyojin/Library/Application Support/typora-user-images/image-20200504202359244.png)

현재는 이렇게 이름과 Git Repository의 이름을 적으면 커밋한 날짜를 캘린더로 보여주는 기능까지 개발했다. 

(View는 차차 고쳐야겠다)



#### Trouble Shooting

##### Build spring & react.js together

회사에서는 back-end만 개발하다보니 front-end와 back-end를 함께 build하려니까 도통 어떻게 해야할 지 모르겠더라. 그래서 이렇게 설정을 해주었다. 

~~~groovy
def webappDir = "$projectDir/front-end"

task yarnInstall(type: YarnTask) {
    workingDir = file("${webappDir}")
    args = ["install"]
}


task yarnBuild(type: YarnTask) {
    workingDir = file("${webappDir}")
    args = ['build']
}

task copyFrontEnd(type: Copy) {
    from 'front-end/build'
    into 'build/resources/main/static/.'
}

task cleanFrontEnd(type: Delete) {
    delete "$projectDir/front-end/build", "$projectDir/front-end/node_modules"
}

yarnBuild.dependsOn yarnInstall
copyFrontEnd.dependsOn yarnBuild
processResources.dependsOn copyFrontEnd
clean.dependsOn cleanFrontEnd
~~~

이 build script를 간단히 설명하자면 위의 `task` 들은 내가 실행해줄 `task` 들을 표기한 것이다. `yarnInstall` 은 `install` command를 실행하려고 만든 것이며, 보면 `type` 이 `YarnTask` 로  되어있다.  



##### Swagger with WebFlux

아쉽게도 Swagger는 webflux의 function type의 router를 [지원하지 않는다](https://github.com/springfox/springfox/issues/2632). swagger로 테스트를 해보고 싶기 때문에 어쩔수 없이 MVC 형태로 붙여서 사용했다. 



##### Swagger with LocalDate

아직 해결 못함!



##### Avoid CORS Error 

~~~java
public class WebConfiguration implements WebFluxConfigurer {
  @Override
  public void addCorsMappings(CorsRegistry registry) {
    registry.addMapping("/**");
  }
  ... 
}
~~~



CORS는 Cross Origin Resource Sharing의 약자로 **도메인** 또는 **포트**가 다른 서버의 자원을 요청하는 것을 말한다. 

하지만 동일 출처 정책(same-origin policy) 때문에 CORS 같은 상황이 발생 하면 외부서버에 요청한 데이터를 브라우저에서 보안목적으로 차단하여 데이터를 정상적으로 받아올 수가 없다.

FE 개발시 debugging을 위해 BE를 8080 띄워두고 FE를 3000으로 띄워서 리소스를 받아오도록 하였는데, 포트가 다르므로 CORS에 해당된다. 차단이 되어 데이터를 받을 수가 없게 되었는데, 이때 `webconfiguration`에서 위처럼 설정해주면 좋다. 다만 실제 production code에서는 이런 코드가 있으면 안되므로 추후 dev 환경에서만 위 설정을 사용하도록 수정해야한다. 



#### 앞으로의 개발

이름만 입력하면 그 사람의 git repo 전부의 commit 기능을 보여주도록 개발할 예정이다. view도 조금더 고치고! 



