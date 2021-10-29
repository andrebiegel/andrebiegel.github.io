---
layout: post
title: Micro-Services Part 1 - What do they solve ?
categories: [Blog]
tags: [microservices ]
date:   2021-11-01

---
 It´s the time that the hype of mircroservices has reached the sector i´m working in. Technically i would like to embrace that. Unfortunuately, i do often see that the hype has fogged what´s really behind that. So here i try to lift the fog. 

A microservice architecture (MSA) is a pattern, which tries to solve a problem. The issue it addresses is scaling.  The pattern uses modularization on a "micro-application level" to achieve that. Before we try to investigate the dimensions the pattern has effects on, we deduce that from the definition Sam Newman gave.  

>  Microservices are independently deployable services modeled around a business domain. They communicate with each other via networks...
>
> -- <cite>Sam Newman</cite>
 
 So the properties of micro services are:
 + independent deployability
 + modelled around a business domain
 + communicating through networks (in other definitions even declared as "with standard protocols")

The basic principle, these properties has been derived from, is divide & conquer. If you have a scaling problem within your application, you should identify the part and work on that. When using the horizontal scaling approach, you need to increase the instances it is running on. To increase the number of instances, you need to have the opportunity to deploy the services (the parts which needs to scale).
But where does the requirement of independance come from? 
The reason for this is the need to be able to scale a MSA itself. Because if an application is going to be torn in serveral parts and these parts form an deployment monolith, the resulting costs in coordination & communication will rise exponentially with an increasing number of micro-services. When creating independent deployable services, this contention risk can be solved. 
So now lets switch from the operational perspective towards development. 
Here independence of micro-services is created by suppressing cross-service changes. This kind of changes symbolize inter-service dependencies, which would end up in a distributed monolith. The state of the art methology of suppressing cross-module changes (the services is a the modularization layer of the pattern) is creating low coupling and high cohesion by using business domains as the unit for modularization. The common technique for creating this kind of modules is Domain Driven Design. The accepted rationale is that changes will be more likely inside of a domain than through serveral business domains
the communication through networks is finally empowering a microservice to be able to choose the process modell as it´s scaling methology. This in turn allows to easily increase the instances by starting new processes.

After explaining the technical dimension of the pattern, we are going to highlight the organisational dimension. If an organizations needs to scale, the overhead in coordinaton and communication will unfortunately grow over time, Applying the pattern means creating creating cross-functional teams and promoting team autonomy. This reduces the disadvantages and limits them to situations where cross module changes occur. In Scale, this inherently leads to towards a shift of the operational ownership of the microservice to the team, because, as more services do exist, there will a time when the operational capacities will be exhausted. This is going to be more likely, when taking into account that the technical dimension of the pattern allows to use more technology stacks. Because it theoretically enables the team to optimize the stack towards the problem the micro-service is going to solve.     

Another consequence of introducing a MSA is that the cost of bringing something into production is crucial. To optimize this aspect an adequate amount of investement has to be done in automation (in CI/CD & resource allocation). A common way to achieve this, is using containers as the base for all services.

So hopefully everybody now has a clear view of what a MSA really is. In the end it is a distributed system and these kind of systems do have their challenges, which should be considered first. i like to sort the challenges into three categories.
 
 * technical challenges: regarding distribution in dimensions of development &  monitoring 
 * organisational challenges: regarding the creating the team structure
 + cultural challenges : regarding to empower the teams to live their new autonomy ("With great power comes great responsibility" ) 
 


## Sources:

* Sam Newman :Monolith to Microservices  (Page 1)

 