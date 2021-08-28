---
layout: post
title: Introduction into keycloak extensions
categories: [Projects]
tags: [Keycloak , IAM, Samples, SPI, Extensions]
date:   2021-08-28
github_url: https://github.com/andrebiegel/keycloak-samples

---

# Introduction into keycloak extensions
During the project I´m currently working on, I had the opportunity to dive into Keycloak. The following is a brief and comprehensive summary of what I have learned so far and which would be also important for you someday.. because usu set keycloak as the de-facto standard IAM solution in their products. Furthermore, many clients do ask for knowledge regarding that product.

Additionally, I was able to extract two types of custom extensions, which we have been using quite extensively in our project. So I will also demonstrate how to add custom JAX-RS Endpoints and custom protocol mappers (eg. for additional JWT claims ) The project itself also includes custom SPIs (service provider interfaces ) and custom JPA extensions. If requested, I can extract/elaborate also on these...

So back to Keycloak in general ... The product is mainly driven by JBoss/RedHat nowadays IBM. Keylcloak is the open-source version of RedHat SSO. The primary use-cases are SAML & OAuth 2 & OIDC SSO scenarios. The base of the product itself is a wildfly application server with an angular UI on top (react js UI is in development).

The first base concept is a realm. A realm manages a set of users, credentials, roles, and groups. Inside of a realm the configuration of partying applications is done via creating clients. The client defines which roles, attributes, and groups a user has in this context. Technically, the integration is done with so-called adapters. Further information about using keycloak can be extracted from the docs. But as a summary, I can tell you .. using keycloak is quite fine. The issues arise when you try to extend it.

The problem lies within the missing implementation details normal developers do not have, when not implementing keycloak in full-time. It starts with the server developer documentation itself because it only contains the direct extension points. The extension API mainly consists of traditional SPI interfaces, which is not that what you would expect, when starting a wildfly java ee application server with an "app". I would recommend remembering that component style by reading the oracle documentation (or just remember to not forget to add the service declarations in META-INF/services and please double-check the typing of the class names or use googles auto service dependency).

But that´s in the end quite straightforward. The main problem is using the internal API. All these nice-looking getters, setters, and domain services but I haven´t found any information about how or when to use what so far. so prepare yourself to be in a NullPointerException bug-hunting session for quite some time when using the API.

After digging at the surface I will now go a bit deeper .. directly jumping to custom Jax rs endpoints in keycloak. As previously mentioned keycloak extensions are based upon service provider interfaces. The Jax Rs Endpoint builds upon the RealmResourceProviderFactory interface.

```java 
public class CustomRealmResourceProviderFactory implements RealmResourceProviderFactory {

    /**
     * base application path of the extension
     */
    @Override
    public String getId() {
        return "custom-jaxrs";
    }

    /** 
     * Keyclaok will use this provider to create the resource object upon each http request 
     */
    @Override
    public RealmResourceProvider create(KeycloakSession session) {
        return new CustomRealmResourceProvider(session);
    }

    @Override
    public void init(Scope config) {
    }

    @Override
    public void postInit(KeycloakSessionFactory factory) {
    }

    @Override
    public void close() {
    }

}
```

It acts as a component entry point. One of its main purposes (besides defining the application path, under which the Resource will be available ) is to make a RealmResourceProvider available in the system, which in turn will be the class, which actually provides a Jax-RS Resource object at runtime.

```java 
public class CustomRealmResourceProvider implements RealmResourceProvider {

	private KeycloakSession session;

	public CustomRealmResourceProvider(KeycloakSession session) {
		this.session = session;
	}

	@Override
	public void close() {
	}

	@Override
	public Object getResource() {
		return new CustomRealmResource(session);
	}

}
```

The Resource Class itself can use the standard Jax-rs annotations/features, but you should not assume that everything is working as it should. For example, I wasn´t able to use @RolesAllowed or SecurityContext out of the box as it should be. The following demonstrates the response of my sample.

 ![alt text](https://github.com/andrebiegel/keycloak-samples/tree/master/images/rest-result.png "Access Token Content")

The next extension is the protocol mapper. Such mapper has the goal to map information into the token. The following sample is an open id connect protocol mapper adding a custom claim into access, Id, or user info token.

```java
public class CustomProtocollMapper extends AbstractOIDCProtocolMapper
        implements OIDCAccessTokenMapper, OIDCIDTokenMapper, UserInfoTokenMapper {

    // Needed to display a generic config dialog in Keycloak
    private static final List<ProviderConfigProperty> configProperties = new ArrayList<ProviderConfigProperty>();

    public static final String PROVIDER_ID = "custom-protocol-mapper";

    static {

        OIDCAttributeMapperHelper.addTokenClaimNameConfig(configProperties);
        OIDCAttributeMapperHelper.addIncludeInTokensConfig(configProperties, CustomProtocollMapper.class);
    }

    public List<ProviderConfigProperty> getConfigProperties() {
        return configProperties;
    }

    @Override
    public String getId() {
        return PROVIDER_ID;
    }

    @Override
    public String getDisplayType() {
        return "custom-protocol-mapper";
    }

    @Override
    public String getDisplayCategory() {
        return TOKEN_MAPPER_CATEGORY;
    }

    @Override
    public String getHelpText() {
        return "custom-protocol-mapper";
    }

    @Override
    protected void setClaim(IDToken token, ProtocolMapperModel mappingModel, UserSessionModel userSession,
            KeycloakSession keycloakSession, ClientSessionContext clientSessionCtx) {
        OIDCAttributeMapperHelper.mapClaim(token, mappingModel,"my Custom Value");
    }
}

```

The Result can be seen in the retrieved token:
![alt text](https://github.com/andrebiegel/keycloak-samples/tree/master/images/sampletoken.png "Access Token Cotent")

So in the end, the extensions themselves are not that scary and even after the NullPointer bug-hunting, it feels quite well, to have done something functioning... I would recommend using the Jax-rs endpoint as a way to extend keycloak basis functionality, maybe as a type of orchestration layer. But please add only the functionality which originally belongs to your IAM domain!

So now to what most you are waiting for.. the code. My Samples are in this repository: https://github.com/andrebiegel/keycloak-samples.

And yes there is so much more to explore and try out  (eg. the documentation states that mappers are also possible with javascript). so feel free to also dive into that topic to the things clients request and add pull requests so that all of us can participate!

greets André

P.S. One More Thing ...

Deployment ... any extension can be hot deployed via the deployments folder, excluding custom SPI implementations. So if you have custom SPIs you do have to use the module import mentioned in the documentation...
## Sources:

* Code https://github.com/andrebiegel/keycloak-samples.git
* https://jwt.io/
* https://www.keycloak.org/docs/latest/server_development/

