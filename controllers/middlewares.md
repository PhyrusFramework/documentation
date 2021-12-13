---
description: Middleware controllers
---

# Middlewares

A middleware is another type of controller that is used as a **wrapper** or a **guard** for the page. The page controller is loaded by a middleware, so different pages may be loaded by the same middleware.

```
class AuthMiddleware extends Middleware
```

Project middlewares are located in /src/middlewares. And we can assign them to a page controller inside the page controller:

```
class PageController extends Controller {

    function init() {
        $this->middleware = Middleware::get('auth');
        // in /src/middlewares/auth/auth.controller.php
        
        // or use an imported class:
        $this->middleware = new MyMiddleware();
    }

}
```

Middlewares will commonly have one of these uses:

* Build a common layout
* Guard logic
* Configurate pages

### Layout middleware

A middleware works exactly like any other controller. With the difference that it has a property named **$controller** which is the controller of the page to display:

```
class MyMiddleware extends Middleware {

    function display() {
        $this->controller->display();
    }

}
```

A middleware, like any other controller, may have a **view.php** file. So we can use it to build the layout:

```
/src/middlewares/website/website.controller.php
/src/middlewares/website/website.view.php:

<header>...</header>
[[ $controller->display() ]]
<footer>...</footer>
```

In this example, the middleware will contain the **header** and the **footer**, which are common parts to all pages. So all pages will use the same middleware.

### Guard middlewares

You can also use a middleware as a **Guard**. A guard validates that you have access to this page or otherwise will **kick** you (redirect) or **block** you (error). Imagine this middleware for an API:

```
class LoggedMiddleware extends Middleware {

    function init() {
        $user = Auth::getUser(); // Get logged user
        
        if ($user == null) { // Not logged
             response_die('unauthorized');    // 401
        }
    }

}
```

### Configuration middlewares

A middleware can also be used to configurate all pages using it, so we don't have to do it manually on each one of them.

For example, previously we learnt that, in order to make an API page (endpoint), we need to return a **raw** body (not html). To do that, we set the controller's raw property to true:

```
class PageController extends Controller {
    function init() {
        $this->raw = true;
    }
}
```

If we build an API, it may become tedious to do that manually for any route. Instead, we can use a middleware to do it for all of them:

```
class APIMiddleware extends Middleware {
    function prepare() {
        $this->controller->raw = true;
    }
}
```

### Nested middlewares

Once again, a Middleware is child class of Controller. This means, that a middleware can do whatever a controller can: have assets, code, view, vue controller.

Therefore, if a controller can have middleware, a middleware can also have a middleware. That's nested middlewares.

In that case, when we access the page, multiple middlewares will be loaded:

```
// /src/middlewares/api
class APIMiddleware extends Middleware { }

// src/middlewares/authenticated
class AuthenticatedMiddleware extends Middleware {
    function init() {
        $this->middleware = Middleware::get('api');
    }
}

// src/pages/api/pages/users   GET /api/users
class UsersEndpoint extends Controller {
    function init() {
        $this->middleware = Middleware::get('authenticated');
    }
}
```

In this example, when we call the endpoint GET /api/users, this will be loaded in this order:

API Middleware > AuthenticatedMiddleware > UsersEndpoint
