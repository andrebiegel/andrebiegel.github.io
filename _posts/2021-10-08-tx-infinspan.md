---
layout: post
title: Technology Experience: Infinispan
categories: [Blog]
tags: [infinispan , development, key-value-store, cache, experience ]
date:   2021-10-08

---
In my last project, I had the pleasure to use infinispan. The use case was a dedicated cache of time series data combined with the expiration feature.
The cache was configured as not persistent and was used as a source to initialize diagrams with that data. It was deployed standalone using docker (image: quay.io/infinispan/server:12.1.6.Final-1).
I had to place the server behind an API-Gateway because I could not get OAuth2 working (see issue link). Luckily it is going to be fixed in version 13. Another issue I faced was regarding the configuration.
I was forced to add a rest-connector in the default endpoint config section. I´m pretty sure that, I have read that, this should not be needed. Nevertheless, in the end, it works pretty well.
So what is my opinion about infinispan? I think infinispan´s primary use cases are within an embedded environment.
That´s my explanation that the OAuth2 issue wasn´t found earlier, because the JWT/OAuth2 thing is pretty common these days.
So do not hesitate to use infinispan. But be careful when using it standalone with features, which are purely built for the standalone use case.

Do you agree? just twitter me (#txinfinispan)... 

## Sources

* Infinispan https://infinispan.org/
* Issue: https://issues.redhat.com/browse/ISPN-13173
