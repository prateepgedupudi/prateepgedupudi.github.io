---
layout:     post
title:      "5 steps to produce SOAP web service with Spring Boot"
subtitle:   "Getting started guide to producing SOAP based web service with Spring Boot"
date:       2017-12-12 02:21:00
author:     prateep_gedupudi
header-img: ""
---

Below is the process of creating a SOAP-based web service with Spring Boot. 
We will be building a web service server that exposes data from some of the Indian states using a WSDL-based SOAP web service.

##### Web service endpoint URL 
[https://pg-produce-spring-boot-soap-ws.herokuapp.com/ws/states.wsdl](https://pg-produce-spring-boot-soap-ws.herokuapp.com/ws/states.wsdl)
##### Code URL 
[https://github.com/prateepgedupudi/spring-boot-producing-soap-ws](https://github.com/prateepgedupudi/spring-boot-producing-soap-ws)

## 1. Create an XML schema to define the domain

## 2. Generate domain classes based on an XML schema

Generate domain classes with the below maven plugin.

````
<plugin>
	<groupId>org.codehaus.mojo</groupId>
	<artifactId>jaxb2-maven-plugin</artifactId>
	<version>1.6</version>
	<executions>
		<execution>
			<id>xjc</id>
			<goals>
				<goal>xjc</goal>
			</goals>
		</execution>
	</executions>
	<configuration>
		<schemaDirectory>${project.basedir}/src/main/resources/</schemaDirectory>
		<outputDirectory>${project.basedir}/src/main/java</outputDirectory>
		<clearOutputDir>false</clearOutputDir>
	</configuration>
</plugin>
````

## 3. Create repository

## 4. Create service endpoint

## 5. Configure web service beans




