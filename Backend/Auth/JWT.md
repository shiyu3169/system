# JWT

JSON WEb Tokens let your identity travel the web securely, but like losing your passport, a stolen JWT ives hackers full access. We will unlock the immense potential of JWTs, and the dangers lurking within.

## What is JWT

JSON Web Tokens, commonly known as JWTs, are a robust method for securely transmitting information between parties as JSON objects. They have become a cornerstone in hte world of web security for good reasons.

## Why is JWT popular

First, it's a lightweight data interchange format that's easy to read and write for humans and simple for machines to parse and generate. It's the backbone of JWTs because it represents its payload, which is where you store the data you want to transmit.

## How does JWT work

JWTs have a structure of three parts: the header, the payload, and the signature. Each section is base64 encoded and separated by a period:

### Header

The header typically consists of the token type, which is JWT, and the algorithm being used, like

- HMAC
- SHA256
- RSA

### Payload

The payload of a JWT is where you store the claims. Claims are statements about an entity, which is typically the user with some additional data. There are three types of claims:

- registered
- public
- private

Registered claims are predefined, like the issuer, expiration time, and subject. While JWT payload can be encrypted using JSON WEB ENcryption (JWE), most implementations use signed but not encrypted tokens. This means that which the data is encoded, it is not encrypted and can be read if intercepted. That's why sensitive information should never travel in a JWT payload unless it's encrypted first.

### Signature

Signing is like sealing an envelope with a wax stamp to ensure it hasn't been tampered with. There are two main types of signing algorithms:

- Symmetric algorithms, like HMAC, SHA256 used a shared secret key for both signing and verification.
- Asymmetric algorithms, such as RSA, use a public/private key pair where the private key signs the token and the public key verifies it.

When choosing an algorithm, consider your needs. Symmetric keys are quick and simple but the secret key must be shared between parties ahead of time. Asymmetric keys allow verification of the creator without sharing private keys but are slower.

Signed JWTs provide authentication, authorization, and secure information exchange. Upon login, the server creates a signed JWT with user details and sends it back. The client uses this to access protected resources by sending the token in the HTTP header.

## When to not use JWT

JWTs are commonly used in standards like OAuth2 and OpenID connect for authentication and authorization. However, it's crucial to know when not to use JWTs. The payload is not encrypted by default so should not contain highly sensitive data. Also, JWTs aren't ideal for managing user sessions since they are stateless. Revoking JWT access can be challenging. Some common vulnerabilities to be aware include token hijacking, where attacker steals a valid JWT to impersonate a user. JWTs also could be vulnerable to cryptographic weaknesses if using weak hashing algorithms. Automated brute force attacks may try to crack token signatures. Automated brute force attacks may try to crack token signatures.

## Mitigate Risk

To mitigate risks when using JWTs, some best practices to follow are:

- keeping JWT payloads compact with only the necessary user claims
- using short token expiration times when possible
- storing tokens securely and invalidating any leaked token
- using strong signature algorithms

## Pros and Cons

The pros are clear, JWTs are self-container, portable, and don't require server-side storage. On the downside, JWTs can be vulnerable to theft. If intercepted, can provide full access to resources. The payload can also get quite large if too much information is included, which can affect performance.

## Summary

Overall, JWTs provide a sclable way to handle authentication, authorization, and information exchange if implemented carefully.
