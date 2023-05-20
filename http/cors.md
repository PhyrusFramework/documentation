---
description: Cross-Origin Resource Sharing
---

# CORS

CORS (**Cross-Origin Resource Sharing**) is a security protocol to control the access of clients to a server via HTTP Requests.&#x20;

CORS needs to be implemented both on Server-Side and Client-Side. That's why you can skip it when you develop a native client, for example developing a native mobile app. However, most browsers nowadays enforce the CORS protocol, so it can be a problem when developing a web-based application.

CORS consists in listing which **Origins** (clients) are allowed to make HTTP requests to the server, and blocking any request coming from a non authorized origin.

To implement CORS, clients / browsers must use **preflight** requests. That means that, whenever a request is made, a previous request with the method **OPTIONS** is sent. When the server receives the OPTIONS request, decides whether the client is allowed or not to access and returns a response (200 OK / 401 Not authorized). If this preflight request is not successful, the real request will never be made by the client, aka, the browser.

If you develop your own client (mobile native app, desktop app) CORS is optional and, being honest, most of developers won't implement it. However, if your application is intended for web (also mobile apps based on webviews, like Ionic), CORS is mandatory because browsers enforce it and you can't disable it, so you'll have to implement it server-side, or requests will be blocked due to the CORS protocol.

Good for you, Phyrus helps with that. CORS is already implemented by Phyrus, and you can configure it in the configuration (**web.yaml --> CORS**):

```
CORS: 
    origin: "*" 
    methods: GET, POST, OPTIONS, PUT, DELETE, PATCH 
    headers: "*" 
    age": 86400
```

By default all origins and headers are allowed. Change that for security reasons if you want.

Also by default all common methods are allowed (GET, POST, PUT, DELETE, PATCH). Add or remove methods here. The Age field specifies how long the cache lasts, 1 day by default.
