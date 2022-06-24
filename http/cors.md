---
description: Cross-Origin Resource Sharing
---

# CORS

CORS (**Cross-Origin Resource Sharing**) is a security protocol to control the access of clients to a server via HTTP Requests.&#x20;

CORS needs to be implemented both on Server-Side and Client-Side. That's why you can skip it when you develop a native client, for example developing a native mobile app. However, most browsers nowadays enforce the CORS protocol, so it can be a problem when developing a web-based application.

CORS consists in listing which **Origins** (clients) are allowed to make HTTP requests to the server, and blocking any request coming from a non authorized origin.

To implement CORS, clients / browsers must use **preflight** requests. That's, whenever a request is made, a previous request with the method **OPTIONS** is sent. When the server receives an OPTIONS request, decides whether the client is allowed or not and returns a response (200 OK / 401 Not authorized). If this preflight request is not successful, the real request will never be made.

If you develop your own client (mobile native app, desktop app) CORS is optional. However, if your application is intended for web (websites or mobile apps based on webviews, like Ionic), CORS is mandatory and you'll have to implement it server-side, or requests will be blocked due to the CORS protocol.

Phyrus helps you with that. CORS is automatically implemented, and you can configure it through the CORS object in the configuration file (web.yaml):

```
CORS: 
    origin: "" 
    methods: GET, POST, OPTIONS, PUT, DELETE, PATCH 
    headers: "" 
    age": 86400
```

Also by default all common methods will be allowed (GET, POST, PUT, DELETE, PATCH). Add or remove methods here.

The Age field specifies how long the cache lasts, 1 day by default.
