---
layout: post
title: Liferay - Shielded Classloading 
categories: [Blog]
tags: [web, dev, liferay, osgi, classloading]
date:   2023-04-28

---

In my daily routine I work very often as a liferay consultant. Liferay has built it´s own ecosystem in the last couple of years. 
Everything is in a OSGI container and so on. 

Unfortunately .. in life .. you always have to life in peace with the surroundings. In IT, it is quite the same, because you can build your ecosystem but customers want to use it their way. 
Another example is the use case of using datasource's from the applicationserver in liferay. Since Liferay 7.4, Liferay has introduced another classloading layer called the "shielded container".
So in order to access resources from the real world you have to use another class loader than before. Be aware of that!
Here is sample from @dnebing blog entry from Liferay.dev.

```java
// get the shielded class loader
ClassLoader shieldedClassLoader = PortalClassLoaderUtil.getClassLoader();

// get the webapp class loader from it
ClassLoader webappClassLoader = shieldedClassLoader.getClass().getClassLoader();

// Set webapp class loader on the thread
thread.setContextClassLoader(webappClassLoader);
```

Anything to disagree or argue with me? just twitter me @BiegelAndre #ShieldedLiferay

## Sources:
* https://learn.liferay.com/w/dxp/liferay-internals/architecture/liferay-classloader-hierarchy
* https://liferay.dev/blogs/-/blogs/setting-up-jndi-in-liferay-7-4

