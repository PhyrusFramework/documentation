---
description: You can choose how to route your pages
---

# API Routing strategies

Routing means to decide what code must be executed depending on the URL being accessed.

Phyrus gives you three different ways or strategies to decide that:

* Automatic routing
* Manual routing
* Route finder

### Automatic routing

If you place your PHP files under the **/back-end/routes** directory, Phyrus will automatically route the page for you by matching the name of the folder with the name of the URI. For instance:

```
https://mysite.com/api/users
```

Would use:

```
/back-end/routes/api/users/index.php
```

### Manual routing

With manual routing, like in other frameworks, you need to manually specify the route and what it does. **Only that here you can use the path to a file, or the action directly**:

```
Router::add('/api/create', Path::back() . '/my-pages/create.php' );

// or
Router::add('/api/create', [
   'GET' => function($req) { ... }
]);
```

### Route finder

The route finder is a method that will be run when the accessed route is not recognized, before falling to **404 Not Found**. In that case you get the route as a string and have like a "last attempt" to decide what to do with it:

```
Router::addFinder(function($route) {

    if ($route == '/not-recognized-route') {
        return Path::back() . '/routes/whatever/index.php';
    }
});
```
