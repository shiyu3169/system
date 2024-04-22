# OAuth 2

Imagine the early days of the internet, sharing info was strightforward. Just hand over your username and password to another service, and they could access anything thyey wanted. This practice is frowned upon these days, but we might still encounter this practice in certain personal finance software to scrape information from crusty old banks. Luckily, we have something much better these days, enter oauth 2.

## What is Oauth 2

Oauth 2 is like giving someone a special key. This key allows them to access specific information in another application. We control who gets access to our data without having to share a password. ANd we can revoke at any time.

Now let's play this out with an example. Consider a photo storage application, SnapStore. We've been using it to store our photos. Now, we want to print some of them using a third-party printer printing service, PrintMagic. Instead of manually uploading each photo to Print Magic, we asked PrintMagic to do the job. WIth a simple click, we grant PrintMagic permission to access our photos on Snap Store. Using OAuth 2, PrintMagic can access our SnapStore photos on our behalf without even knowing our SnapStore login credentials. This is an example of oauth flow. It's an elegant stance between us, PrintMagic and SnapStore which all orchestrated by Oauth 2.

Now, let's unpack this further. In this context, we are the resource owner because we own our photos on SnapStore. SnapStore is the resource server that stores our photos. PrintMagic is the client that wants to access the photos. The authorization server could be a part of SnapStore or an external identity provider and is responsible for handling the oauth 2 process.

Let's follow the OAuth 2 flow in this scenario. It begins when we instruct PrintMagic to fetch photos from SnapStore. PrintMagic sends a client ID and scope while represent the access level to SnapStore authorization server. As a resource owner, we authenticate directly with SnapStore and grand PrintMagic the consent to access our photos. Once concent is granted, the authorization server sends an anthorization code back to PrintMaigc. PrintMagic then presents this authorization code, client ID and client sercret to the authorization server. The client secret is a private key shared only between PrintMagic and authorization server. If the authorization server verifies the authorization code, client ID and client secret, it issues an access token to PrintMagic. Finally, PrintMagic uses this access token to request our photos from SnapStore's resource server.

## Why use Oauth 2

This Oauth 2 process ensures our SnapStore login credentials are never exposed to PrintMagic while allowing PrintMagic to access photos we authrozied it to see. It's also important to know that the access token can be set to expire after a certain time or can be revoked by us at any point providing an additional layer of security. Oauth 2 also support refresh tokens which can be used to obtain a new access token when the old one expires without requiring our intervention.

## Summary

That's OAuth 2 in a nutshell. It's an essential piece of the web security and infrastructure and the backbone of many secure seamless app interactions we use daily.
