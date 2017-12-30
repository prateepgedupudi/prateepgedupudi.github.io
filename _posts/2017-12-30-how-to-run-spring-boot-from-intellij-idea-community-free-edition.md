---
layout: post
title: IntelliJ IDEA Community(Free) Edition for Spring Boot Applications in 2018
subtitle: Increase Your Spring Boot Productivity with (Free) IntelliJ IDEA Community Edition
date: 2017-12-30T07:29:14.512Z
author: prateep_gedupudi
header-img: img/bg_post_spring_boot_intellij.jpg
---
As many of us are aware Spring recommended the `STS(Spring Tool Suit)` for Spring Boot development. You might aware STS is based on the Eclipse platform and loosing its popularity due to issues in it, on other hand IntelliJ is increasing user base day by day. We have two different editions in IDEA, one is `Community Edition` which is free version and an other one is `Ultimate Edition` which is paid version. I strongly believe that the Community Edition is more than sufficient for Spring Boot development.    

If you are already using STS and thinking to switch to `IntelliJ IDEA` with out spending money on Ultimate Edition (paid version) then `IntelliJ IDEA Community Edition` is the best choice. Initially you may feel discomfort to work with IDEA due to shortcuts differences from STS. But trust me, once you habituated with IDEA then you feel more productive especially in code completion, version control, etc. You can achieve everything with out leaving IDEA.

One of the important reason behind using STS for Spring Boot is `Run/Debug as Spring Boot Application`. Many of us don't know, how STS is able to provide `Run/debug as Spring Boot Application` feature. It is through a `maven/gradle` Spring Boot `plugin` which usually available in `POM.xml/build.gradle` when ever we create a Spring Boot project either from STS or from [`Spring Initializr`](https://start.spring.io/). So `Run as Spring Boot Application` is a task in maven/gradle.  

````
<build>
	<plugins>
		<plugin>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-maven-plugin</artifactId>
		</plugin>
	</plugins>
</build>
````

````
apply plugin: 'org.springframework.boot'
````

Now you might have an answer for a question about running Spring Boot App in IntelliJ IDEA Community edition. Yes, you are right. Just Run/Debug maven/gradle task. Here are the screen shots of the tasks for spring boot maven and gradle apps with in Intellij IDEA . 
<img class="img-responsive center-block" src="/img/maven_spring_boot_runas.png" alt="">
<img class="img-responsive center-block" src="/img/gradle_run_as_spring_boot.png" alt="">

