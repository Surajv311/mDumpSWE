
# SAML 

A SAML (Security Assertion Markup Language) provider is a system that helps a user access a service they need. There are two primary types of SAML providers, service provider, and identity provider.
- A service provider needs authentication from the identity provider to grant authorization to the user.
- An identity provider performs the authentication that the end user is who they say they are and sends that data to the service provider along with the user’s access rights for the service.

Microsoft Active Directory or Azure are common identity providers. Salesforce and other CRM solutions are usually service providers, in that they depend on an identity provider for user authentication.

SAML works by passing information about users, logins, and attributes between the identity provider and service providers. Each user logs in once to Single Sign On with the identify provider, and then the identify provider can pass SAML attributes to the service provider when the user attempts to access those services. The service provider requests the authorization and authentication from the identify provider. Since both of those systems speak the same language – SAML – the user only needs to log in once.

OAuth is a slightly newer standard that was co-developed by Google and Twitter to enable streamlined internet logins. OAuth uses a similar methodology as SAML to share login information. SAML provides more control to enterprises to keep their SSO logins more secure, whereas OAuth is better on mobile and uses JSON.

Facebook and Google are two OAuth providers that you might use to log into other internet sites.

[What is saml _al](https://www.varonis.com/blog/what-is-saml)


----------------------------------------------------------------------





















