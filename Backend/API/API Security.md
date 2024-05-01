# API Security (WIP)

APIs are the backbone of modern web applications. They allow different software systems to communicate and share data. However with increased connectivity comes to risk of security vulnerabilities. That's why it's critical to implement robust security measures to protect APIs and sensitive data they handle.

## HTTPS

HTTPS is the security version of HTTP, which encrypt data transmitted between the client and ser4ver. This encryption helps prevent eavesdropping, man-in-the middle attacks, and other security threats. With HTTPS, sensitive information like API Keys, session tokens and user data are protected from preying eyes.

## OAuth 2

OAuth2 is an industry standard authorization protocol. Instead of sharing credentials directly, it allows users to grant 3rd party application's limited access to their resources. Here is a typical OAuth2 flow:

1. Client application initiates the process by redirecting the suers to the authorization server like Google or Facebook.
2. The user authenticates with the authorization server and grants permission to the client app to access specific resources
3. The authorization server then issues an access token to the client app.
4. The client app uses this access token to make API calls to API on behalf of the user.
5. Our API which is the resource server validates the token and responds with the requested data or action

So no credential are ever shared, just temporary access token. This way, we don't have to store user passwords and securely integrate with 3rd party services. Popular use cases including logging in with Google or Facebook, accessing cloud storage, or connecting to email or calendar apis.

Let's look at a concrete example. Say we build a travel app that needs access to the users Google Calendar to check availability. With OAuth2, our app redirects the user to Google to authenticate and Grant calendar access. Google then provides an access token that our app can use to read that users calendar events from the Google Calendar API. All without you storing usernames or passwords .

## WebAuthn

WebAuthn is a newer standard that provide a more secure and user friendly way of authenticating users. It replaces traditional password based authentication with public key cryptography and biometric factors like fingerprints or facial recognition. This makes it much harder for attackers to compromise user accounts through techniques like fishing or credential stuffing. WebAuthn is supported by major browsers and platforms making a robust and future proof authentication solution for APIs.

## API keys

API keys are common way to authenticate an server to serve service communications, such as when a backend service need to access 3rd party APIs or our own internal APIs. However, using a single API key fo all services and operations can be risky. Instead, Implement API keys with varying access levels where each key has specific permissions and scopes defined. For example, we could have a read-only key for public data access, a write key for modifying internal data stores, and an admin key for privileged operations like deploying and updates. This way, even if one API key is compromised, attacker's access is limited only to the operations allowed by that keys level. We minimized the blast radius compared to using a single master key. It's also a good practice to rotate API keys periodically and have an easy way to revoke compromised key immediately. Some services also let us configure expiration times for API keys. Authorization is the process of determining what resources and actions a client is allowed to access perform. Even if a client is authenticated, they should only be able to access and modify the data they authorized for. A common pattern is to use role based access control, where clients are assigned roles with specific permissions. For example, a viewer may be able to read data, while an editor can also modify it. Proper authorization ensures that our API follows the principle of leaz privilege minimizing the potential attack service.

## Rate limiting

Another important security measure is rate limiting which controls the number of requests a client can make within a given time period. This helps protect our apis from being overwhelmed by malicious actors or buggy clients making excessive requests. Rate limiting rules can based on various factors like IP address, user ID, or API key. We can also have different rate limits for different types of requests or resources. For example, we might allow more read requests than write requests per second. Rate limiting improves security and helps maintain the performance and availability of your APIs.

## API Versioning

API versioning is a best practice that allows us to evolve the API overtime while maintaining backward compatibility. With versioning, we can introduce breaking changes or new features without disrupting existing clients. This is typically done by including the version number in the API endpoint url. Client can then choose which version to use, and we can deprecate older versions when ready. Versioning also helps with better change management and documentation. As each version can have it's own set of requirements and specifications.

## AlowListing

AlowListing is a security technique where it will explicitly allow access only to a predefined set of trusted entities, such as IP addresses, user IDs or API keys. Everything else is denied by default. This appoach follows the principle of "deny all", which is more secure than a DenyListing approach where we deny a few known bad actors and allow everyone else. In the context of APIs, we can implement AllowListing ruloes based on various criteira, such as allopwing only specific IP randers to access certain endpoints or limiting access to certain resources based on user roles or permissions.

## OWASP

The open web application security project provides valuable reousrces and guidelines for web applicaion security including API secruity. OWASP has identified documented the top 10 critical seurity risk for apis, such as broken object level authorization, security misconfiguration, and more. It's essential to review and address this risk during the design and development phases of our API to ensure a secure FOundation. We can leverage OWASP resources, such as the API security top 10 list to access our API vulnerabilities and imprement appropriate counter measures.

## API Gateway

An API Gateway access a single entry point for clients to access our backend services and apis. It provides a centralized layer for enforcing security policies where limiting authentication and other coresscutting converns. By using an API Gateway, we can abstract away the complexity of managing these security features across individual services or apis. API Gateway also offer additional benefits like traffic management, caching, logging, and monitoring. Making them a valuable component in mordern application architectures.

## Error handling

Proper error handling is crucial for API security and user experience. When errors occur, we want to provide clients with descriptive yet secure error messages. For example, instead of a vague internal server error, a good error message could be "fail to retrieve user data, please check that you are authenticated and have sufficient permissions". This gives the client enough information to troubleshoot without exposing sensitive details. For instance, instead of an error message exposing that we using SQL and there may be an ejection vulnerability by saying something like "SQL query failed due to malformed input containing a DROP TABLE command", a better approach would be a generic "invalid input provided. Please review and try again". It's generally good to categorize error as client errors, such as validation failures or server errors, and return appropriate status codes like 400 bad request or 500 internal server error. Never ever return full stack traces or expose internal error message or codes in production, as this can be valuable information for attackers. The goal is to help legitimate clients while protecting sensitive information and attack vectors.

## Input Validation

The final tip is to implement robust input validation for all data received from clients. This includes validating request parameters, headers, payloads, and any other user supply inputs. Failing to validate input can lead to various vulnerability, like SQL injection, cross-site scripting attack, and other injection attacks. Input validation should be done on both the client side and the server side. As client side validation alone is not sufficient. On the server side, we can use dedicated input validation libraies or frameworks to enforce strict validation rules and sanitize user input. It's also a good practice to centralize and standardize our validation logic either though an API Gateway or a separate validation service.
