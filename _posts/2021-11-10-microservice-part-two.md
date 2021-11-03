---
layout: post
title: Microservices Part 2 - Is it a good choice for you?
categories: [Blog]
tags: [microservices, architecture, design, pattern ]
date:   2021-11-10

---
 In part 1 of the series digged into the question, what a microservice architecture really is and what kind of properties and consequences it has. I assume this fundamental understanding and will now deduce from that, who, from a general point of view, should   be cautious when evaluating a microservice archetecture for him/herself.

Just to have a short summary of the important things so far: 

+ microservices should be be independently deployable
+ microservices are modelled around a business domain
+ microservices communicate over networks
+ result in technical, organisational & cultural challenges 

So from general point of view .. when might be your plan of a distributed system  not the rigth choice ? One simple anwser is ..every time when the challenges cannot be faced the rigth way.  A possible example is costumer-managed software. Just think about the following.. a costumer received several versions as a simple web archiv file (War) und just needs to deploy that or uses an simple zip to extract a preconfigured application-server. Imagine the reactions if the costumers downloads a ton of new service runtimes and a huge documentation about how to install that thing. i would forecast that the it department of the customer migth have some issues about that. The same can be transferred towards a situation in the context of a project for individual software (WORT prüfen). If the service provider creates a solution running on a container plattform and the costumer does not have any experiences with that, the solution seems to be ill-fated.

## Sources:

* Sam Newman :Monolith to Microservices

 