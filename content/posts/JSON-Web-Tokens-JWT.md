---
 	layout: post
 	title: JSON-Web-Tokens-JWT
 	date: 2021-01-01
 	draft: false
 	tags: []
---

# JSON-Web-Tokens-JWT[1*9pWUdYPAwCQoWdEnvZli4A.jpeg](JSON%20Web%20Tokens%20(JWT)%2086fe6818c9384adab0f151f589d48ce7/19pWUdYPAwCQoWdEnvZli4A.jpeg)
> JSON Web Token (JWT) Is a JSON object and it is considered one of the safest ways to transfer information between two participants.
To create it, you need to define a header with general information on the token, payload data, such as the user id, his role, etc.
First, the user logs on to the authentication server using an authentication key (it can be a *username / password* pair , or a *Facebook* key, or a *Google* key, or a key from another account).
The *JWT header* contains information on how the *JWT* signature should be calculated .
A header is also a *JSON* object that looks like this:
> header = { “alg”: “HS256”, “typ”: “JWT”}
>
It will be used when creating the signature.
In the example the authentication server creates a *JWT* with information about the **userId**
> payload = { “userId”: “b08f86af-35da-48f2–8fab-cef3904660bd” }
>
There is a list of standard *applications* for *JWT* payload — here are some of them:
- *iss* (issuer) — defines the application from which the token is sent.
> // header eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9// payload eyJ1c2VySWQiOiJiMDhmODZhZi0zNWRhLTQ4ZjItOGZhYi1jZWYzOTA0NjYwYmQifQ// signature -xN_h82PHVTCMA9vdoHrcZxH-x5mb11y1537t3rGzcM
>
Now that we have all three components, we can create our *JWT*
const token = encodeBase64Url(header) + ‘.’ + encodeBase64Url(payload) + ‘.’ + encodeBase64Url(signature)
// JWT Token //eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOiJiMDhmODZhZi0zNWRhLTQ4ZjItOGZhYi1jZWYzOTA0NjYwYmQifQ.-xN_h82PHVTCMA9vdoHrcZxH-x5mb11y1537t3rGzcM
**You can try to create your own *JWT* Online *[jwt.io](https://jwt.io/)* .
