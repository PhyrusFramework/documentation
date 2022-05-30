# Middlewares

Middlewares are filters that can be used in several routes to prevent the access to a route, for example to check if the user is logged in or if he has enough permissions or role to perform this action.

Like routes, middlewares can be created **automatically** or **manually**.&#x20;

To create a route automatically, create a file inside **/back-end/middlewares** returning a function that will **return false** to prevent the access:

```
// /back-end/middlewares/auth.php

return function($req) {
   if (!$enough_permissions) {
      return false;
   }
}
```

Alternatively you can also create the middleware manually somewhere else:

```
Router::addMiddleware('auth', function($req) {
   if (!$enough_permissions) {
      return false;
   }
});
```

### Use the middleware in routes

To use the middleware, you can do it globally for all methods in a route, or locally for a single method:

```
// Globally
return [
    'middleware' => 'auth',
    
    'GET' => function($req) {...},
    'POST' => function($req) {...}
];

// Locally
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
