---
layout: post
date:   2019-10-01 22:00:00 +0200
title:  "Web Development: Configuration via Web-Components"
categories: [Blog]
tags: [frontend-development, configuration, Web-Components, JavaScript ]
---

As as consequence of my posts x & and y, the following idea came into my mind..why not using the markup language itself as fundament of a configuration provider. The following markup would suggests a solution.

```html
<app-config localstorage="true">
  <app-config-entry value="value" key="key" type=""></app-config-entry>
</app-config
```
The possibilities to use SSE & ESI garanties integration scenarios for self-contained-systems (SCS), PWAs and other SPA-like solutions. Furthermore the custom html element enables implementing addtional functions like localstorage based resolution orders.

