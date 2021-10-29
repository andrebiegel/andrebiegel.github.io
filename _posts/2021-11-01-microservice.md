---
layout: post
title: Micro-Services Part 1 - What do they solve ?
categories: [Blog]
tags: [microservices ]
date:   2021-11-01

---
It´s time that the hype of microservices has reached the sector I´m working in. Technically I would like to embrace that. Unfortunately, I do often see that the hype has fogged what´s really behind that. So here I try to lift the fog.

A microservice architecture (MSA) is a pattern, which tries to solve a problem. The issue it addresses is scaling. The pattern uses modularization on a "micro-application level" to achieve that. Before we try to investigate the dimensions the pattern has effects on, we deduce that from the definition Sam Newman gave.

>  Microservices are independently deployable services modelled around a business domain. They communicate with each other via networks...
>
> -- <cite>Sam Newman</cite>
 
 So the properties of microservices are:
+ independent deployability
+ modelled around a business domain
+ communicating through networks (in other definitions even declared as "with standard protocols")
The basic principle, these properties have been derived from, is divide & conquer. If you have a scaling problem within your application, you should identify the part and work on that. When using the horizontal scaling approach, you need to increase the instances it is running on. To increase the number of instances, you need to have the opportunity to deploy the services (the parts which need to scale).
But where does the requirement of independence come from? 
The reason for this is the need to be able to scale an MSA itself. Because if an application is going to be torn into several parts and these parts form a deployment monolith, the resulting costs in coordination & communication will rise exponentially with an increasing number of micro-services. When creating independently deployable services, this contention risk can be solved. 
So now let's switch from the operational perspective towards development. 
Here independence of micro-services is created by suppressing cross-service changes. These kinds of changes symbolize inter-service dependencies, which would end up in a distributed monolith. The state of the art methodology of suppressing cross-module changes (the services is the modularization layer of the pattern) is creating low coupling and high cohesion by using business domains as the unit for modularization. The common technique for creating this kind of module is Domain Driven Design. The accepted rationale is that changes will be more likely inside of a domain than through several business domains
the communication through networks is finally empowering a microservice to be able to choose the process model as its scaling methodology. This in turn allows to easily increase the instances by starting new processes.
After explaining the technical dimension of the pattern, we are going to highlight the organisational dimension. If an organization needs to scale, the overhead in coordination and communication will, unfortunately, grow over time, Applying the pattern means creating cross-functional teams and promoting team autonomy. This reduces the disadvantages and limits them to situations where cross-module changes occur. In Scale, this inherently leads to towards a shift of the operational ownership of the microservice to the team, because, as more services do exist, there will be a time when the operational capacities will be exhausted. This is going to be more likely when taking into account that the technical dimension of the pattern allows using more technology stacks. Because it theoretically enables the team to optimize the stack towards the problem the micro-service is going to solve.
Another consequence of introducing an MSA is that the cost of bringing something into production is crucial. To optimize this aspect an adequate amount of investment has to be done in automation (in CI/CD & resource allocation via self-services ). A common way to achieve this is by using containers as the base for all services.

Of course, MSA can provide a few benefits more. Because when the cost to introduce features is quite low (by the means that only needed parts have to be changed and tested and nothing more) it can result in a reduced time to market. Otherwise, when using the process model to scale, it will allow scaling the application in a cost-effective way. 


So hopefully everybody now has a clear view of what an MSA really is. In the end, it is a distributed system and these kinds of systems do have their challenges, which should be considered first. I like to sort the challenges into three categories.

 
* technical challenges: regarding distribution in dimensions of development,logging, tracing, monitoring,operations
* organisational challenges:  regarding the creating the team structure,transfering service-ownership 
* cultural challenges: empowering the teams to live their new autonomy ("With great power comes great responsibility" ), transfering service-ownership

In the next part of my MSA series, I will try to answer the question regarding when an MSA is a good choice.


Is anything left open? Just twitter me and we will find a solution .. @BiegelAndre #msapart1
 


## Sources:

* Sam Newman :Monolith to Microservices  (Page 1)

 