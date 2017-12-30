---
layout: post
title: IntelliJ IDEA Community(Free) Edition for Spring Boot Applications in 2018
subtitle: Increase Productivity with (Free) IntelliJ IDEA Community Edition Spring Boot
date: 2017-12-30T07:29:14.512Z
author: prateep_gedupudi
header-img: /img/bg_post_spring_boot_intellij.jpg
---
As many of us are aware Spring recommended the `STS(Spring Tool Suit)` for Spring Boot development. You might aware STS is based on the Eclipse platform and loosing its popularity due to issues in it, on other hand IntelliJ is increasing users base day by day. We have two different editions in IDEA, one is `Community Edition` which is free version and an other one is `Ultimate Edition` which is paid version. I personally feel that Community Edition is more than sufficient for Spring Boot development.    

If you are already using STS and thinking to switch to `IntelliJ IDEA` with out spending a single `$` on it then `IntelliJ IDEA Community Edition` is the best choice. Initially you may feel discomfort to work with IDEA due to shortcuts differences from STS. But trust me once you habituated with IDEA then you feel more productive especially in code completion, git, etc. 

One of the important reason behind using STS for Spring Boot is `Run/Debug as Spring Boot Application`. Many of us don't know, how STS is able to provide `Run/debug as Spring Boot Application` feature. It is through a `maven/gradle` Spring Boot `plugin` which usually available in `POM.xml/build.gradle` when ever we create a Spring Boot project either from STS or from \[https://start.spring.io/](Spring Boot Initializer). So `Run as Spring Boot Application` is a task in maven/gradle.  

```
<build>
```

```
	<plugins>
```

```
		<plugin>
```

```
				<groupId>org.springframework.boot</groupId>
```

```
				<artifactId>spring-boot-maven-plugin</artifactId>
```

```
		</plugin>
```

```
	</plugins>
```

```
</build>
```

Now you might have an answer for a question about running Spring Boot App in IntelliJ IDEA Community edition. Yes, you are right. Just Run/Debug maven/gradle task. Below is the screen shot of running spring boot maven app with in Intellij IDEA . 

![null](/img/maven_spring_boot_runas.png)

\
