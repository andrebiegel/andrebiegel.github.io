---
layout: post
title: Evaluating Technologies for project usages - React, Vue or Angular ? 
categories: [Blog]
tags: [architecture , frontend, development, maintenance, react, vue, angular, architecture , evaluation]
date:   2021-09-24

---
![comparing react, angular and vue](https://iotvnaw69daj.i.optimole.com/AXVzL2w.n2y9~6666f/w:509/h:259/q:90/dpr:2.0/https://www.codeinwp.com/wp-content/uploads/2019/01/angular-vs-vue-vs-react.jpg "comparing react, angular and vue")

As a member of the architecture expert group at USU / DSS (Consulting unit of USU), the following types of questions exist all the time. Can we use framework x, y, or Z in project w?

The questions arrive when, most of the time, a specific problem solution is already designed. This is based upon the fact that, when searching through the internet, developers have only their problem in their minds and nothing else. Functionally everything is already set. This is fine. Because functionality is the basis for every project usage. The problem should be fixable with the chosen technology before further investigations appear. 

Unfortunately, there are a few more dimensions to test the framework against before it can be used in an enterprise project for a customer. I would like to demonstrate a bit of that with the common SPA frameworks out there. So I would like to evaluate React, Vue, and Angular. The first thing I´m checking is the license. In this case, all 3 have MIT licenses. So there is no issue with that. The next and the most overseen is, what I call, "project liveness". Especially when using community-driven open source projects, it is important to look at the project and its members. The goal is to assess the project regarding its stability. the number of contributors is a good start. Furthermore, you should look at who is actually contributing most of the time. Is it spread among? Or centralized towards only a few or maybe just one? You may ask, why is this important? In an enterprise context, clients need stable technologies to rely on. Because the solutions have to last a few years. So the projects need to be maintained for that time, So it is not a good sign when the amount of contributors is quite low and even worse when the real contribution (the most of the code) is being made by just one developer. What if that developer loses the interest/ has no time or dies? (aka the "bus factor")? Not every company has the resources to compensate that by employees, who can dive into the project and have the time to gain the knowledge to maintain it by themself. Of course, this is only the beginning. The usage of the project can also help to answer the stability question. Is the project used by big players? This raises the possibility that the project will be supported by these companies. Additionally what is about the stability of the releases themselves? Does the project produce releases with breaking changes every week? So how do these frameworks handle these? Considering the number of contributors, Vue is definitely behind React and Angular especially in version 3. Additionally, when examining the contributing members, even more, Vue is mainly built by only one developer. All 3 are used by big players, so this one is fine.

What about the release stability? Reacts version history tells stories. Between version 16 and 17 are 3 years!

| Version | 15 | 16 | 17 |
|---|---|---|---|
| Year | 2016 | 2017 | 2020 |

Angular has published its release practices. 

> All major releases are typically supported for 18 months.
> * 6 months of active support, during which regularly-scheduled updates and patches are released.
> * 12 months of long-term support (LTS), during which only critical fixes and security patches are released.

So with Angular, you will have a higher maintenance cost than with React (if React keeps their promise: "We value API stability."). When considering Vue, the version strategy is not that clear; because it does not follow semantic versioning (breaking changes in minor changes possible), which raises maintenance costs, especially when considering that the release cycle is irregular (3.2 in August, 3.1 in June, 3.0 in September 2020). 

To sum the stability up ... React seems to be pretty stable, followed by angular and last but not least Vue.

But can you take this as the result and recommend react for your spa projects? I have only considered a few external dimensions. There are also internal ones. So does your organization has developer know-how? And more than one developer, please ... developers can leave ... Has your organization a strategic decision towards a framework?

In the end, there is very much to consider before using new technologies in projects. But as a starting point, I would suggest React. From an overall non functional perpective and in my context of consulting in projects for individual software solutions; it seems to fit pretty well. 

Have you anything to adjust or do have an other result? Just twitter me with #spacomparison

## Sources

* Image from https://www.codeinwp.com/blog/angular-vs-vue-vs-react/
* Contributions Vue  https://github.com/vuejs/vue-next/graphs/contributors
* Release practice Angular : https://angular.io/guide/releases
* React Js Design Principles: https://reactjs.org/docs/design-principles.html