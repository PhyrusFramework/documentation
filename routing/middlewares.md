# Middlewares

Middlewares are guards who decide whether the user can or not access a route, and they can be reused for multiple routes with different purposes. The most common use of middlewares is to check the authentication and block the access if the user is not logged or has not the necessary role. But it can be used with other purposes.

A middleware is basically a **function**. If this function **returns false**, the access will be **blocked**. Alternatively, the middleware can also end the execution with an error code (400, 401, 403, 404...)

Like routes, middlewares can be detected **automatically by the directory structure** or **be manually created by the developer**.&#x20;

To create a route automatically, just create a file inside **/back-end/middlewares** returning a function that will **return false** to prevent the access:

```php
// /back-end/middlewares/auth.php

return function($req, $params) {
   if (!isLogged())
      return false;
}
```

Alternatively you can also define the middleware manually somewhere else by name:

```php
Router::addMiddleware('auth', function($req, $params) {
   if (!$logged)
      return false;
});
```

### Use the middleware in routes

A middleware can be used globally for a whole route (all of its methods) or specifically for a method:

```php
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

Sometimes you would want to combine multiple middlewares to reuse code, instead of repeating it. For this purpose, you can use **Router::useMiddleware**:

```php
Router::addMiddleware('my-custom', function($req) {

   // First check if user is logged using the other 'auth' middleware
   if (Router::useMiddleware('auth') === FALSE) {
      return false;
   }
   
   // Now do something else
   ...

});
```
