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

If you look the below schema closely then you can easily identify that we have two elements(`getStateRequest, getStateResponse`) and one complex type(`state`). 
One element is for Request object and an other is for Response object. Request object carries the `ID` of the state while coming in and hitting the service end point URL.
On other hand Response object carries back the whole State object to the client which includes state details. That is the reason to include state complex type in to response object.
While coming to the `state` complex type, it holds `id, name, population, capital and language` for a state.        
````
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:tns="http://prateep.info/spring/soapws"
           targetNamespace="http://prateep.info/spring/soapws" elementFormDefault="qualified">

    <xs:element name="getStateRequest">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="id" type="xs:string"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>

    <xs:element name="getStateResponse">
        <xs:complexType>
            <xs:sequence>
                <xs:element name="state" type="tns:state"/>
            </xs:sequence>
        </xs:complexType>
    </xs:element>

    <xs:complexType name="state">
        <xs:sequence>
            <xs:element name="id" type="xs:string"/>
            <xs:element name="name" type="xs:string"/>
            <xs:element name="population" type="xs:int"/>
            <xs:element name="capital" type="xs:string"/>
            <xs:element name="language" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>

</xs:schema>
````

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




