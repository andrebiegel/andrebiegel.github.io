---
layout: post
title: Microservices - Choreography vs Orchestration 
categories: [Blog]
tags: [web, dev, choreography, orchestration ,microservices]
date:   2021-12-22

---

The following question reached me as a member of the architecture expert group at USU DSS: What do you think about choreography and orchestration in the context of microservices?

To answer this one, I would like to, firstly, shortly explain the two approaches and will then highlight the contrary characteristics. 

So let´s start with the things in common. Both approaches tackle the task of distributed transactions (the saga pattern).

But the way they achieve the problem is contrary. Orchestration handles the execution of the transaction with the help of a service. So, a centralized workflow engine handles the steps of the transaction. What are the pros & cons of that? The centralized style allows to centrally capture (source controlled) the state/progress of the workflow. This consequently leads to the fact, that the workflow can also be easily monitored and errors/retries/timeouts are centrally manageable. The participating services do not need to know the overall workflow. On the other side, the services need to know about compensation of their own parts, because these parts have to be also controlled by the orchestrator service. The centralized services form a single point of failure, which has to be taken into account when considering error scenarios of the whole system. At runtime, the orchestrator services form a monolithic system. The ability of your services to be independently deployable will therefore suffer when using this approach.

The contrary approach is a decentralized one, called choreography. Here the use of domain events in combination with the event-carried-state transfer pattern is used to transfer the responsibility of managing the transaction/workflow (and it´s compensation) from one service to all participating services. Here every part of the transaction has to implement its own part from the whole workflow. The benefits are obvious. The services remain loosely coupled, even at runtime, and can, therefore, be scaled and changed without any problems. There is no single point of failure. On the other side, the workflow progress is implicitly hidden. Also, the monitoring is pretty hard and needs, like any other features a centralized solution offers pretty directly further services. 

So when to choose what?
The question can be reduced to the problem "centralized vs. decentralized". This is actually the same as the question of when to use microservices or not. The answer is always, yes if it solves your problem? Do you have a problem? Why don´t just start small and centralized? And when this solution starts to make issues react to them. The decentralized solution might sound more challenging. But keep in your mind! Before you solve any super technical issues, start with the business domain. Model your workflow, implement the compensation in your services and leverage the features the tooling has out of the box (like monitoring). So are there edge-cases? Yes there are... just think about cross-cutting workflows (through several bounded contexts and therefore quite often through several teams)
Here the decentralized solution might have advantages you should not ignore. But in the end, it is a question of how much cross-team dependencies can be handled easily. 

The common tool I see quite often in the context of orchestration is camunda bpm. But that might be my bias ... What are you using? apache airflow? 

So to sum that up:

+ choose orchestration inside of bounded contexts
+ choose choreography otherwise

Anything to disagree or argue with me? just twitter me @BiegelAndre #OrchVsChoreo

## Sources:

* Sam Newman :Monolith to Microservices
* https://camunda.com/de/
 