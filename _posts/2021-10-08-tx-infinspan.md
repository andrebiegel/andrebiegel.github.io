---
layout: post
title: Technology Experience: Infinispan
categories: [Blog]
tags: [infinispan , development, key-value-store, cache, experience ]
date:   2021-10-08

---
In my last project, i had the pleasure to use infinispan. The use-case was a dedicated cache of time series data combined with the expiration feature.
The cache was configured as not persistent and was used as a source to initialize diagrams with that data. It was deployed standalone using docker (image : quay.io/infinispan/server:12.1.6.Final-1). 
I had to place the server behind an API-Gateway, because i could not get OAuth2 working (see issue link). Luckily it is going to be fixed in version 13. Another issue i faced, was regarding the configuration.
I was forced to add an rest-connector in the default endpoint config section. I´m pretty sure that, i have read that, this should not be needed. Nevertheless, in the end it works pretty well
So what is my opinion about infinispan?  Actually i think, inifinispan´s primary use cases are within an embedded environment.
That´s my personal explanation that the OAuth2 issue wasnt found earlier, because the JWT/OAuth2 thing is pretty common these days. 
So do not hesitate to use infinispan , but be carefull when using it standalone with features, which are purely build for the standalone usecase. 

Do you agree? if not just twitter me (#txinfinispan)

## Sources

* Infinispan https://infinispan.org/
* Issue : https://issues.redhat.com/browse/ISPN-13173
