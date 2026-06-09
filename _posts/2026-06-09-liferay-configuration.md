# The Liferay Configuration Framework - The hidden gems   

The liferay configuration framework is a framework that allows you to configure liferay applications via osgi mechanisms. It is a very traditional development approach and provides integration in the settings ui of liferay. 100% Java-based. In my GitHub repository I provided a few examples a few years ago. Last week a customer of mine asked me about how to do configuration for a classical java osgi service. That was one of these situations where I was able to provide a link to my repo and say there is everything you need. But when I was looking through the repository, I recognized that the code I provided was quite old and needs some additional work to be up to date. 

So this was the reason why I started to overhaul my GitHub repository.

In this post I will provide some information about the framework you won't find in the official documentation.
 We start with the basic steps that have to be made when creating a configuration bundle. Don't panic, I will not start about how to write a java interface. The first issue is very classical. You are working for a client which has not a Liferay workspace in his repository. Then the dependency hell starts. But BOMs (Bill of Materials) are here to save your life. Liferay has one nowadays.

```Xml
<dependency>
    <groupId>com.liferay.portal</groupId>
    <artifactId>release.dxp.bom</artifactId>
    <version>2026.q1.7</version>
    <type>pom</type>
    <scope>import</scope>
</dependency>
```
And remember to use the Liferay artifact repository. Maven central is not up to date.

```Xml
<repository>
    <id>liferay-maven</id>
    <url>https://repository.liferay.com/nexus/content/repositories/public/</url>
    <name>Liferay Maven Repo</name>
</repository>
```
But the most important thing is to use the correct bnd directives to create a functional configuration bundle. 
The directives are the following: 

```
# old directive
-metatype: *
# new in dxp 7.4.0
-metatype: *
-plugin.metatype=com.liferay.ant.bnd.metatype.MetatypePlugin
```

I found the directive while examining the situation that my Maven build was not working and a corresponding Gradle build with a liferay workspace was working. So I looked in the generated bnd file (a sample is shown below). The bnd file is packed with additional directives. So if you have an issue, which can be narrowed down to a build time issue, you might want to check that file in your tmp directory of the Gradle build. I found the file in the following path (*build\tmp\jar*).


```
-add-resource=D\:/github/liferay-n2f3/liferay-n2f3/liferay-scoped-company/build/tmp/compileJSP,D\:/github/liferay-n2f3/liferay-n2f3/liferay-scoped-company/build/jspc
-antbnd.jspanalyzer.fallback-javaee-package=jakarta
-cdiannotations=
-consumer-policy=${replacestring;${range;[\=\=,\=\=]};.*,(.*)];$1}
-contract=*
-donotcopy=(.*.wsdd)
-fixupmessages.classpath.empty=Classpath is empty
-fixupmessages.deprecated=annotations are deprecated
-fixupmessages.unicode.string=Invalid unicode string
-includeresource.compileInclude=
-jsp=*.jsp,*.jspf,*.jspx
-liferay-service-xml=service.xml,*/service.xml
-metatype=*
-noclassforname=true
-plugin.bundle=com.liferay.ant.bnd.resource.bundle.ResourceBundleLoaderAnalyzerPlugin
-plugin.liferay=com.liferay.ant.bnd.resource.AddResourceVerifierPlugin,com.liferay.ant.bnd.jsp.JspAnalyzerPlugin,com.liferay.ant.bnd.metatype.MetatypePlugin,com.liferay.ant.bnd.npm.NpmAnalyzerPlugin,com.liferay.ant.bnd.resource.bundle.ResourceBundleLoaderAnalyzerPlugin,com.liferay.ant.bnd.sass.SassAnalyzerPlugin,com.liferay.ant.bnd.service.ServiceAnalyzerPlugin,com.liferay.ant.bnd.social.SocialAnalyzerPlugin,aQute.lib.spring.SpringComponent,com.liferay.ant.bnd.spring.SpringDependencyAnalyzerPlugin,com.liferay.ant.bnd.enterprise.EnterpriseAnalyzerPlugin
-plugin.metatype=com.liferay.ant.bnd.metatype.MetatypePlugin
-provider-policy=${replacestring;${range;[\=\=,\=\=]};.*,(.*)];$1}
-removeheaders=Bnd-LastModified
-sass=*
-sources=true
Bundle-Name=de.abiegel.configuration.osgi.company
Bundle-SymbolicName=de.abiegel.configuration.osgi.company
Javac-Debug=on
Javac-Deprecation=off
Javac-Encoding=UTF-8
archivesBaseName=de.abiegel.configuration.osgi.company
buildTreePath=\:liferay-scoped-company
description=de.abiegel.configuration.osgi.company
displayName=project '\:liferay-scoped-company'
distsDirName=distributions
docsDirName=docs
environmentFileDir=.
environmentName=local
group=liferay-n2f3
libsDirName=libs
liferay.workspace.product=dxp-2026.q1.6-lts
liferay.workspace.target.platform.version=
name=liferay-scoped-company
path=\:liferay-scoped-company
portal.version=7.4.x
propertiesPluginEnvironmentFileDirProperty=environmentFileDir
propertiesPluginEnvironmentNameProperty=environmentName
propertiesPluginGradleUserNameProperty=gradleUserName
status=integration
testReportDirName=tests
testResultsDirName=test-results
version=unspecified
```

The next undocumented feature of the framework is the possibility to import configurations from bundles via a bundle. This is very useful if you want to deploy configurations by default and don't want to deploy them via the */mnt/liferay/files/osgi/configs* (mount directory) folder of the liferay image. 

For this purpose you have to use the following directive in your bnd file.

```
Liferay-Configuration-Path: /<configuration folder in bundle>
```

Additionally, the framework provides the feature to create custom configuration categories by implementing the *ConfigurationCategory* interface. If you also want to have a nice icon, like Liferay does, for your configuration category, you can use the clay icon system with the implementation of the *getCategoryIcon()* method. The icon has to be a valid clay icon name. You can find a list of all available icons in the clay documentation. 

```java
@Component
public class FooCategory implements ConfigurationCategory {

	@Override
	public String getCategoryKey() {

		return "my-foo-company";
	}

	@Override
	public String getCategorySection() {
		return "my-foo-title";
	}

	@Override
	public String getCategoryIcon() {
		return "third-party";
	}
}
```
The next feature I want to highlight is the possibility to use variables in the configuration. The interpolation of system properties is a relatively old feature of the framework. But it is still very useful. New in that area is the possibility to use liferay environment variables. Liferay environment variables are prefixed with *LIFERAY_*. So the following definition in your config file will read a custom environment variable.
Also new is the possibility to use the *\$[]* square brackets to interpolate the value of a variable via the interpolation plugin of apache felix configadmin (see the documentation of the framework). 
By the way, the usage of variable interpolation is a bit tricky. Because the data of the configuration file will only be used if you have nothing saved in the ui. If you want to enter the variable in the ui, you have to escape the *\{\}* braces and brackets. Or you have to import the configuration file via the _osgi/configs_ directory. Otherwise, the interpolation will not work, also the import via the former mentioned bnd-directive will not work. Additionally, the interpolation with the *\$[]* square brackets will not show the value in the ui. The variable not rendering on the UI is the expected behavior. In a clustered environment, different nodes may have different values to display. Keeping it as a variable in the UI signals to the admin that it is environment-specific.  

```properties
defaultLiferayEnvProp="${LIFERAY_MY_CUSTOM_ENV_PROPERTY}"
# apache felix interpolation plugin feature
defaultEnvVar=$[env:PATH] 
```

Another thing you need to know before using the framework, is the need to have unique language keys for each configuration of configuration category. So if you have two configuration items with the same language key, the second one will overwrite the first one.

The standard and recommended best practice to prevent this is to ensure that all language keys are unique across different modules. A robust method is to prefix language keys with a unique identifier, such as the module's bundle symbolic name or the fully qualified class name of the configuration interface.

For example, instead of a generic key like:

```properties
configuration.name=My Configuration
```
A unique key would be:

```properties
com.acme.my.module.one.configuration.name=My First Configuration
```
And for the second module:
```properties
com.acme.my.module.two.configuration.name=My Second Configuration
```

This practice guarantees that each configuration's labels will be displayed correctly and predictably, regardless of the deployment order of the modules.

When implementing configurations in portlets, there is one issue when following the documentation. The default values of the config set via Systems Settings will not be transferred to the portlet. So you have to set the default values in the portlet configuration page. But there is a way to fix this. You can implement a _ConfigurationPidMapping_  class. After that the default values will be transferred to the portlet settings.

```java
@Component
public class MyConfigurationPidMapping implements ConfigurationPidMapping {
	
	@Override
	public Class<?> getConfigurationBeanClass() {
		return ConfiguredComponentConfig.class;
	}
	@Override
	public String getConfigurationPid() {
		return "de_abiegel_configuration_osgi_example_OsgiConfiguredPortlet";
	}
}
```

The last thing I want to mention is the possibility to use the osgi spec configuration style. This is done by using only the annotations of the osgi specification. The result is a configuration that is treated as a system-scoped configuration and displayed in the settings ui under the third-party category in the section _Plattform_. At the moment, when i'm writing this, liferay has a few issues with this feature. But I communicated the things to the support team, and they are working on it (LPD-93602, LPD-82478).

# Sources

* https://github.com/abiegel/liferay-configuration-api
* https://learn.liferay.com/w/dxp/security-and-administration/administration/configuring-liferay/configuration-files-and-factories/using-configuration-files
* https://learn.liferay.com/w/dxp/development/traditional-java-based-development/core-frameworks/configuration-framework
* https://www.clayui.com/docs/components/icon
* https://learn.liferay.com/kb-article/how-to-use-environment-variables-for-passwords-within-osgi-config-files
* https://github.com/apache/felix-dev/tree/master/configadmin-plugins/interpolation

Keywords: Liferay, OSGI , BND, Configuration Framework , DXP 7.4.0, 2026.q1.7

