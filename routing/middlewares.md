# Middlewares

Middlewares are filters that can be reused in multiple routes with different purposes. For example, to check authentication and block access if user is not logged. But it can be used with other purposes.

A middleware is basically a **function**. If this function **returns false**, the access will be **blocked**.

Like routes, middlewares can be created **automatically by the filesystem** or **manually**.&#x20;

To create a route automatically, just create a file inside **/back-end/middlewares** returning a function that will **return false** to prevent the access:

```
// /back-end/middlewares/auth.php

return function($req) {
   if (!$logged)
      return false;
}
```

Alternatively you can also create the middleware manually somewhere else:

```
Router::addMiddleware('auth', function($req) {
   if (!$logged)
      return false;
});
```

### Use the middleware in routes

To use the middleware, you can do it globally for all methods in a route, or specifically for each method:

```
// Globally
return [
    'middleware' => 'auth',
    
    'GET' => function($req) {...},
    'POST' => function($req) {...}
];

// Specifically
return [
    'GET' => function($req) {...},
    
    'POST' => [
        'middleware' => 'auth',
        function($req) {
            ...
        }
    ]
];

// Combined
return [
    'middleware' => 'no-auth',
    'GET' => function($req) {...},
    
    'POST' => [
        'middleware' => 'auth',
        function($req) {
            ...
        }
    ]
];
```

{% hint style="info" %}
In this last example, the route with the POST method will only use the **auth** middleware, not the other (no-auth).
{% endhint %}

### Nested middleware

Sometimes you would want to combine multiple middlewares so you reuse the code, instead of repeating it. For this purpose, you can use **Router::useMiddleware**:

```
Router::addMiddleware('my-custom', function($req) {

   // First check if user is logged using 'auth' middleware
   if (Router::useMiddleware('auth') === FALSE) {
      return false;
   }
   
   // Now do something else
   ...

});
```
