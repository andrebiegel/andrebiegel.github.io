---
layout: post
title: Liferay DXP 7.4. 2025.q1 JSF Support now reactivated 
categories: [Blog]
tags: [web, dev, jsf, liferay, dxp]
date:   2026-02-27

---
## 🚀 Liferay 7.4 DXP 2025.Q1 LTS -- JSF with THIN Deployment and Annotation-Based Portlets

With the **2025.Q1 LTS release of Liferay DXP 7.4**, starting from
Docker tag:

`2025.q1.19-lts`

Liferay significantly modernizes JSF portlet development.

The biggest improvement?\
You can now replace traditional XML descriptor files entirely with
**Java annotations**.

That means no more:

-   ❌ `portlet.xml`
-   ❌ `liferay-portlet.xml`
-   ❌ `liferay-display.xml`

Instead, everything can be configured directly in your Java code.

------------------------------------------------------------------------

### 🧠 Goodbye XML -- Hello Annotations

In previous Liferay versions, creating a JSF portlet required multiple
XML descriptor files:

-   `portlet.xml`
-   `liferay-portlet.xml`
-   `liferay-display.xml`

These files were often verbose, redundant, and error-prone.

With **Liferay 7.4 DXP 2025.Q1 LTS**, you can now define everything
using annotations such as:

-   `@PortletConfiguration`
-   `@LiferayPortletConfiguration`
-   `@InitParameter`
-   `@SecurityRoleRef`

This dramatically reduces configuration overhead and aligns JSF portlet
development with modern Jakarta EE best practices.

------------------------------------------------------------------------

### 🧩 Annotation-Based Portlet Example

Here is a real-world example of how a JSF portlet can now be fully
configured using annotations:

``` java
@PortletConfiguration(
  portletName = GenericFacesPortletImpl.PORTLET_NAME,
  displayName = {@LocaleString("Search Prime JSF Portlet")},
  initParams = {
    @InitParameter(
      name = "javax.portlet.faces.defaultViewId.view",
      value = "/WEB-INF/views/view.xhtml"
    )
  },
  roleRefs = {
    @SecurityRoleRef(roleName = "administrator"),
    @SecurityRoleRef(roleName = "power-user"),
    @SecurityRoleRef(roleName = "user"),
    @SecurityRoleRef(roleName = "guest")
  }
)
@LiferayPortletConfiguration(
  portletName = GenericFacesPortletImpl.PORTLET_NAME,
  properties = {
    "com.liferay.portlet.ajaxable=false",
    "com.liferay.portlet.display-category=USU",
    "com.liferay.portlet.instanceable=true",
    "com.liferay.portlet.requires-namespaced-parameters=true"
  }
)
```

#### What This Replaces

  Old XML File            Now Replaced By
  ----------------------- --------------------------------
  `portlet.xml`           `@PortletConfiguration`
  `liferay-portlet.xml`   `@LiferayPortletConfiguration`
  `liferay-display.xml`   Annotation properties

All portlet metadata is now:

-   Co-located with the implementation\
-   Type-safe\
-   Refactor-friendly\
-   Easier to maintain

------------------------------------------------------------------------

### 🐳 THIN Deployment -- Lean and Modern

Combined with the new **THIN deployment model**, JSF portlets are now:

-   Smaller\
-   Cleaner\
-   Easier to deploy\
-   Free from heavy descriptor packaging

Example Docker command:

``` bash
docker run -it -p 8080:8080 liferay/portal:2025.q1.19-lts
```

The runtime already provides the required JSF infrastructure --- your
module only contains your business logic and configuration annotations.

------------------------------------------------------------------------

### 🔍 Example Repository

A working example of this new approach can be found here:

https://github.com/andrebiegel/liferay-jsf-portlet

The repository demonstrates:

-   JSF portlet for 7.4 DXP 2025.Q1 LTS\
-   No XML descriptors\
-   Annotation-only configuration\
-   Clean Maven setup\
-   Ready for Docker-based deployment

------------------------------------------------------------------------

## 💡 Why This Matters

This change represents a major step forward:

-   🚀 Less boilerplate\
-   🧹 Cleaner architecture\
-   🔧 Easier maintenance\
-   📦 True lightweight deployment\
-   🏗 Modern Jakarta-style configuration

For teams maintaining legacy JSF portlets with complex XML descriptors,
this release offers a clear path toward modernization.

------------------------------------------------------------------------

## 📦 Required JSF Bridge Dependencies (Separate Bundle Deployment)

When using JSF with THIN deployment in Liferay 7.4 DXP 2025.Q1 LTS, it is important to understand that certain JSF bridge and component libraries are not packaged inside your portlet artifact.
Because they are declared as compileOnly, they must be deployed separately as OSGi bundles to the Liferay runtime.
Example dependency configuration:

```
compileOnly "com.liferay.faces:bridge-api:6.0.0"
compileOnly "com.liferay.faces:bridge-ext:8.0.2"
compileOnly "com.liferay.faces:bridge-impl:6.0.1"
compileOnly "com.liferay.faces:jakarta.faces:2.3.21.LIFERAY-PATCHED-1"
compileOnly "com.liferay.faces:primefaces:15.0.6.LIFERAY-PATCHED-1"
```
Why compileOnly?

Using compileOnly ensures that:

-  Your portlet remains lightweight
-  No duplicate JSF bridge classes are packaged
-  The runtime provides shared implementations

Version conflicts are avoided

What Must Be Deployed?

The following artifacts need to be available as OSGi bundles inside Liferay:

- bridge-api
- bridge-ext
- bridge-impl
- Liferay-patched jakarta.faces
- Liferay-patched primefaces

These bundles can be:

- Placed in the /deploy folder
- Included in your Docker image
- Managed via a dedicated infrastructure module

This approach keeps your portlet truly THIN, while the JSF bridge infrastructure is provided once at the platform level — exactly how modern modular OSGi applications are designed to work.

## 📦 Conclusion

**Liferay 7.4 DXP 2025.Q1 LTS** introduces:

-   Native JSF support\
-   THIN deployment\
-   Full annotation-based portlet configuration\
-   Elimination of `portlet.xml`, `liferay-portlet.xml`, and
    `liferay-display.xml`

JSF development on Liferay is now leaner, cleaner, and more aligned with
modern Java standards.

Happy coding 🚀
 

