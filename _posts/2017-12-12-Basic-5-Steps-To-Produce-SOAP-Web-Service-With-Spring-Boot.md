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
Prerequisite step is to create spring boot project with [`Spring Initializr`](https://start.spring.io/) with `Web Services` and `Web` dependencies.
`WSDL4J` is Java stub generator for WSDL. Include wsdl4j dependency in `POM.xml`.

````
<dependency>
    <groupId>wsdl4j</groupId>
    <artifactId>wsdl4j</artifactId>
</dependency>
```` 

##### Web service endpoint URL 
[https://pg-produce-spring-boot-soap-ws.herokuapp.com/ws/states.wsdl](https://pg-produce-spring-boot-soap-ws.herokuapp.com/ws/states.wsdl)
##### Code URL 
[https://github.com/prateepgedupudi/spring-boot-producing-soap-ws](https://github.com/prateepgedupudi/spring-boot-producing-soap-ws)

## 1. Create an XML schema to define the domain

First step is to create XSD for a domain. If you look the below schema closely then you can easily identify that we have two elements(`getStateRequest, getStateResponse`) and one complex type(`state`). 
One element is for Request object and an other is for Response object. Request object carries the `ID` of the state while coming in and hitting the service end point URL.
On other hand Response object carries back the whole State object to the client which includes state details. That is the reason to include state complex type in to response object.
While coming to the `state` complex type, it holds `id, name, population, capital and language` for a state.
An other important info need to be noted is `targetNamespace="http://prateep.info/spring/soapws"` which will be used as a package while generating domain classes.        

`Location: src/main/resources/states.xsd`

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

Next step is to generate domain classes for above XSD. Manual effort of creating domain classes is not at all recommended.
So we have a `maven` plugin to create domain classes automatically while building the project. 
If you monitor the configuration closely, we have  `schemaDirectory` where the plugin looks for the schemas and `outputDirectory` where plugin generates domain classes.
Generated classes are placed in `src/main/java/info/prateep/spring/soapws` directory due to name space `http://prateep.info/spring/soapws` we have given in `states.xsd`

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

Next step is to provide data to the web service. 
Best way of dealing with data in spring is create a repository. Lets create a `StateRepository`.
As of now implementation with hardcoded data. If we want, we can integrate with `database` in this step.

````
package com.ticktuts.springbootproducingsoapws;

import org.springframework.stereotype.Component;
import info.prateep.spring.soapws.State;
import org.springframework.util.Assert;

import javax.annotation.PostConstruct;
import java.util.HashMap;
import java.util.Map;

@Component
public class StateRepository {
    private static final Map<String,State> states = new HashMap<>();

    @PostConstruct
    public void initData() {
        State ap = new State();
        ap.setId("AP");
        ap.setCapital("Amaravathi");
        ap.setName("AndhraPradesh");
        ap.setLanguage("Telugu");
        ap.setPopulation(52000000);
        states.put(ap.getId(),ap);

        State tl = new State();
        tl.setId("TL");
        tl.setCapital("Hyderabad");
        tl.setName("Telanga");
        tl.setLanguage("Telugu");
        tl.setPopulation(52000000);
        states.put(tl.getId(),tl);

        State ka = new State();
        ka.setId("KA");
        ka.setCapital("Bangalore");
        ka.setName("Karnataka");
        ka.setLanguage("Kannada");
        ka.setPopulation(52000000);
        states.put(ka.getId(),ka);

        State tn = new State();
        tn.setId("TN");
        tn.setCapital("Chennai");
        tn.setName("Tamilnadu");
        tn.setLanguage("Tamil");
        tn.setPopulation(52000000);
        states.put(tn.getId(),tn);
    }

    public State findState(String id) {
        Assert.notNull(id, "State id must not be null");
        return states.get(id);
    }
}
````

## 4. Create service endpoint

Next step is to create `StateEndpoint` which is a `POJO` with a few Spring WS annotations to handle the incoming SOAP requests and responding with the responses.
It is very important to know about below spring annotations.

`@Endpoint` registers the class with Spring WS for processing incoming SOAP messages.

`@PayloadRoot` used by Spring WS to pick the handler method based on the message namespace and localPart.

`@RequestPayload` indicates that the incoming message will be mapped to the method’s request parameter.

`@ResponsePayload` makes Spring WS map the returned value to the response payload.

````
package com.ticktuts.springbootproducingsoapws;

import info.prateep.spring.soapws.GetStateRequest;
import info.prateep.spring.soapws.GetStateResponse;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.ws.server.endpoint.annotation.Endpoint;
import org.springframework.ws.server.endpoint.annotation.PayloadRoot;
import org.springframework.ws.server.endpoint.annotation.RequestPayload;
import org.springframework.ws.server.endpoint.annotation.ResponsePayload;

@Endpoint
public class StateEndpoint {
    private static final String NAMESPACE_URI = "http://prateep.info/spring/soapws";

    private StateRepository stateRepository;

    @Autowired
    public StateEndpoint(StateRepository stateRepository) {
        this.stateRepository = stateRepository;
    }

    @PayloadRoot(namespace = NAMESPACE_URI, localPart = "getStateRequest")
    @ResponsePayload
    public GetStateResponse getState(@RequestPayload GetStateRequest request) {
        GetStateResponse response = new GetStateResponse();
        response.setState(stateRepository.findState(request.getId()));

        return response;
    }
}
```` 

## 5. Configure web service beans
Next step is configuration through `WebServiceConfig`. 
So that all the beans declared in this class will be available in the `ApplicationContext`.
It is important to inject and `setApplicationContext` to `MessageDispatcherServlet`. Without that, Spring WS will not detect Spring beans automatically.
It is also important to notice that we need to specify bean names for `MessageDispatcherServlet` and `DefaultWsdl11Definition`. Bean names determine the URL under which web service and the generated WSDL file is available.
If you are running locally then the WSDL will be available under `http://localhost:8080/ws/states.wsdl`.
Configuration `servlet.setTransformWsdlLocations(true)` uses the WSDL location from the servlet transformation. 

`Finally we can run our application as Spring Boot App or package as jar and run as java application.`

````
package com.ticktuts.springbootproducingsoapws;
import org.springframework.boot.web.servlet.ServletRegistrationBean;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.core.io.ClassPathResource;
import org.springframework.ws.config.annotation.EnableWs;
import org.springframework.ws.config.annotation.WsConfigurerAdapter;
import org.springframework.ws.transport.http.MessageDispatcherServlet;
import org.springframework.ws.wsdl.wsdl11.DefaultWsdl11Definition;
import org.springframework.xml.xsd.SimpleXsdSchema;
import org.springframework.xml.xsd.XsdSchema;

@EnableWs
@Configuration
public class WebServiceConfig extends WsConfigurerAdapter {
    @Bean
    public ServletRegistrationBean messageDispatcherServlet(ApplicationContext applicationContext) {
        MessageDispatcherServlet servlet = new MessageDispatcherServlet();
        servlet.setApplicationContext(applicationContext);
        servlet.setTransformWsdlLocations(true);
        return new ServletRegistrationBean(servlet, "/ws/*");
    }

    @Bean(name = "states")
    public DefaultWsdl11Definition defaultWsdl11Definition(XsdSchema statesSchema) {
        DefaultWsdl11Definition wsdl11Definition = new DefaultWsdl11Definition();
        wsdl11Definition.setPortTypeName("StatesPort");
        wsdl11Definition.setLocationUri("/ws");
        wsdl11Definition.setTargetNamespace("http://prateep.info/spring/soapws");
        wsdl11Definition.setSchema(statesSchema);
        return wsdl11Definition;
    }

    @Bean
    public XsdSchema statesSchema() {
        return new SimpleXsdSchema(new ClassPathResource("states.xsd"));
    }
} 
````

<div class="embed-responsive embed-responsive-16by9">
	<iframe width="960" height="720" src="https://www.youtube.com/embed/SiFSNtDAIS0" frameborder="0" gesture="media" allow="encrypted-media" allowfullscreen></iframe>
</div>