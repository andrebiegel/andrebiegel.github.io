---
layout: post
title: Microservices Part 2 - Is it a good choice for you?
categories: [Blog]
tags: [microservices, architecture, design, pattern ]
date:   2021-11-10

---
In part 1 of the series, I dug into the question, what a microservice architecture really is and what kind of properties and consequences it has. I assume this fundamental understanding and will now follow up the matter about, who, from a general point of view, should be cautious when evaluating a microservice architecture for him/herself.

Just to have a short summary of the important things so far: 

+ microservices should be independently deployable
+ microservices are modeled around a business domain
+ microservices communicate over networks
+ result in technical, organizational & cultural challenges

So from a general point of view .. when might be your plan of a distributed system, not the right choice? One simple answer is ..every time when the challenges cannot be faced the right way. A possible example is a customer-managed software. Just think about the following. A customer received several versions as a simple web archive file (WAR) and just needed to deploy that or used a simple ZIP to extract a preconfigured application server. Imagine the reactions if the customer downloads tons of new service runtimes and huge documentation about how to install that thing. I would forecast that the IT department of the customer might have some issues with that. The same can be transferred towards a situation in the context of a project for individual software (WORT prüfen). If the service provider creates a solution running on a container platform and the customer does not have any experience with that, the solution seems to be ill-fated. Another problem arises when using the approach in an environment, where the business domains cannot be clearly identified. Every product evolves. Especially in a startup context when the product is trying to open up a market. The normal process would be that the startup will test which features are demanded and which are not. So the business domain and the resulting bounded contexts are in a state of self-discovery. In such a situation, does it look like a good strategy to accept the challenges, instead of using a monolithic approach with a corresponding faster time-to-market? I personally do have a similar situation quite often. A client has a vague vision of a system in the context of process digitalization or wants to expand their product portfolio. Nowadays the idea of microservices is actually extremely spread in the minds of the stakeholders. This often leads towards a technical decision up-frond. Unfortunately, these clients are extremely hard to lead back towards a system architecture that addresses the actual needs. Yes if the idea will bring them a huge number of customers, a microservice architecture, might be the right choice. But is this the right decision at the current point in time? Have these customers feedback whether the idea is really working? Or is the functional alignment going to be shifted towards the end-user, which is actually willingly paying for the new service or product? Can this only be evaluated during being in production with an MVP/ prototype or does the customer has enough information to decide that up-front? You might get the clue that .. YES I do love technical challenges ... but in the end ... does it provide value/ROI?
You might remember my words in the last part of this series .. microservices do solve a problem. Do you have a problem? Do you have a good reason, despite being trendy?

From my personal experience, I do hear the following:

+ We want to enhance the maintainability of the system, MSA will allow us to separate parts and will minimize changes in the whole system
+ we want to reduce time-to-market, MSA will allow us to bring new features faster by just adding new mircoservices
+ we would like to improve team autonomy: with a MSA we can move ownership into teams
+ with a MSA we can scale cost-effectively
+ we need MSA because we need to scale our developers
+ we need to enhance robustness .. MSA is the rigth way to do that
+ we need to embrace new technologies .. MSA allow us  try dem out in manner to be able to have fast rollbacks

Do not misunderstand me, all of these can be good reasons to do microservices. but will it be the right choice for you in your context? 
The already mentioned reasons can also be adressed alternatively. Have you also evaluated these solutions ? 

* The very often mentioned maintainability mainly adresses an issue of the modularization of your application. A Modulith/ modular Monolith can be a better solution.
* reduce time to market -- analyse the complete software development lifecycle; maybe the bottleneck is not the development, may be requirement engineering ?  
* team autonomy: another approaches of bringing responsibility to the tean can be .. using a modular monolith as a direct technical strategy regarding a part of the business domain or another way would be the declaration of specific technical decision-makers (for UI, DB ... ). Or try to reduce dependencies upon the operations team by provoding self service approaches for the provisioning ? 
* instead of scaling the application pieces, a vertical scaling for hole application can be a starting point. Or horizontal scaling with classic load balancer, or replace technology with better one
* To tackle needed robustness  you could just run the app behind a load balancer. 
* scale devevlopers. Try a modulith
* The need to use new technologies can also addressed by using polyglot environmments.


I hope you get the point. Microservices are not the silverbullet. And you probably are not the best match like a scale-up. A business with a clear domains and a rising number of customers.

The mext part will then try to give a vision of how  microservices can be introduced. 


## Sources: 

* Sam Newman :Monolith to Microservices
 
