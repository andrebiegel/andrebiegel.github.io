---
layout: post
title: REST - Custom Verbs in Googles Rest API 
categories: [Blog]
tags: [web, dev, rest]
date:   2023-04-28

---

I received a question regarding the expert group of the company I work for. The question is whether Custom Verbs from the Google REST API are REST compatible or not, and whether this is now considered state of the art. The context is that a customer needed consulting on API design for their REST API.

Here's my response:

First of all, Google defines the use of custom verbs as follows: "They should only be used for functions that are difficult to accomplish with standard methods. In general, API designers should prefer standard methods whenever possible." I understand this approach primarily as an exception to the rule of using standard HTTP verbs. To better understand what such a use case looks like, I took a look at the Google Ads REST API. The following example is given:

"One reason the API uses custom methods is to enable batch processing of multiple operations in a single API request. When using strict REST semantics, only one campaign can be updated at a time. A conventional REST update to a campaign, for example, would require sending an HTTP PATCH request per campaign resource."

Thus, this is a definition of a custom operation on a resource.

The next step is to revisit the definition of a resource.

Fielding defines it as follows:

"a resource R is a temporally varying membership function MR(t), which for time t maps to a set of entities, or values, which are equivalent."

To come back to the Google Ads example explicitly:

"https://googleads.googleapis.com/v13/customers/1234567890/campaigns:mutate"
Here, one may wonder to what extent the conceptual resource matches the explicit one. Shouldn't one explicitly name the process that is hidden behind the mutate method and performs operations on the set of campaigns, thus creating a real resource that can be created with a PUT? Hopefully, you can see where I'm going with this. Essentially, custom verbs are not REST compatible based on this example, as they would then have to be a custom HTTP method. But people are afraid to do this because they don't know how the internet will react when strange HTTP verbs are sent around that nobody knows.

The Ads API uses them for bulk operations that would have to be explicitly named to be a real resource according to Fielding.

The Google Cloud documentation also describes custom verbs in connection with the HTTP GET verb. They speak of:

"For example, the HTTP GET verb should be used by custom methods that implement special resource views." I understand their example as a method for specifying the resource representation. And this can actually be solved with custom content types in the standard.

So, I don't see any non-mappable construct with this requirement at the moment.

As I mentioned before, the RPC style is generally not REST according to Fielding. The ways of the style would be either a meaningful resource or Fielding also defines the option of "control-data" in the body of a request, which more precisely specifies the operation on the resource.

That's enough theory for now. The question of state of the art is different. Because, although Fielding can always be used as a reference, pure REST systems are rare in practice. He defines HATEOS as a constraint, and few systems meet this. This is why there is the maturity model. Meanwhile, I tried to find out what others are doing - Spotify, Twitter, Facebook - but as you have already found out, this approach by Google is not very common. However, my selection may not be representative because the APIs I found are often focused on OLAP (i.e., queries). Facebook has completely migrated to GraphQL. GraphQL has become increasingly popular in recent times, but it doesn't quite fit the use case because the use of custom verbs only makes sense for operations
Google is not an unfamiliar name when it comes to driving technologies on the web (think Speedy and HTTP2). Therefore, I would tell customers that this may not be about the "state of the art" status, but at most about the "early adapter" area. Google defines it as an exception to the rule and wants to save requests that go against the resource. As mentioned before, this can be addressed with a specific resource... So, the question is actually: What does the customer want to use it for? If they want to introduce an RPC-style, they can do it, but then it's not REST, and it doesn't have to be. If it works for the customer, why not.


Anything to disagree or argue with me? just twitter me @BiegelAndre #RESTCustomVerbs

## Sources:
* 
* https://cloud.google.com/apis/design/custom_methods?hl=de#http_mapping
* https://developers.google.com/google-ads/api/rest/design/service-methods?hl=de
* https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm
* https://martinfowler.com/articles/richardsonMaturityModel.html

