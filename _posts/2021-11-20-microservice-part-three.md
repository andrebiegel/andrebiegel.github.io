---
layout: post
title: Microservices Part 3 - Summary
categories: [Blog]
tags: [microservices, architecture, design, pattern ]
date:   2022-07-20

---
 In part one and two of the series i answered the questions what a microservice architecture really is, what kind of properties and consequences it has and which considerations have to be made, when evaluating the approach. 
 So now is the time to speak about the how can a microservice architecture be introduced.
 Here im not going to differenciate between a migration and green-field scenario. But if you have read my last part, you hopefully have well defined arguments for your decision. The migration patterns themself are described pretty well in Sam Newman´s Monolith to Microservices. My perspective is bit more focusing on the overall goals.

 So my recommendations will build upon the following:
Its important to integrate all parts as fast as possible. This is actually a first test of all processes , starting at build and ending with provisioning.  It will also enable you to communicate and practically show the progress of your project. If one of your processes hurts , do it more often. And regarding provisioning , keep it simple; start small, start with the processes your teams already master. Do not underestimate the efford to build and manage kubernetes clusters, even if kubernetes is so common in microservices reports.
But to be able to do this, the primary developemnt phase has to be supported with the introduction of logging (eg with the elastic stack, former known as the ELK stack) If the amount of your services grows, your teams will also request a centrallized tracing solution (a solution here might be jaeger). The introduction of a metrics solution like prometheus, migth be a business use case and should be therefore also in your backlog. 

The recommendation about starting small can also be applied upon the hole process of a microservice architecture (MSA). One propery of doing small changes is the need to prevent breaking changes. breaking changes spreads through several services instances and makes small changes to big ones, which are by definiton difficult to manage and rollback.
 The fact that a MSA is a global pattern delivers the truth that thers is no silverbullet regarding a MSA. Every MSA is a specific solutions towards it ´s individual requirements, regarding team structure, knowledge in the teams, company processes and business requirements and so on. another consequence of its individual nature a MSA has, is the need make only small changes in the architecure. the smaller the steps are ,the less it costs to roll them back. Because you will make mistakes. better be prepared for that. A consequence of that, you need the environment to make mistakes, so your company needs to have the specific culture , A culture that also accepts that a MSA is a evolutionary process (if it has a certain size) which cannot be planed up front in a big bang style, which is pretty common these days. 

## Sources:

* Sam Newman: Monolith to Microservices

 