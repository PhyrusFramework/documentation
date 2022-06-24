---
description: Use dynamic parameters in the URL for routing
---

# Dynamic routing

Dynamic routing refers to using dynamic parameters in the route, such as:

* /profile/:userId
* /project/:projectId/members

All routing strategies mentioned before allow this feature.

### Automatic routing

Automatic routing here works exactly as in Nuxt for front-end. Use directories starting with \_ to specify that it's a dynamic parameter:

```
/profile/:userId

/back-end/routes/profile/_userId/index.php
```

### Manual routing

In the case of manual routing, parameters are specified with a **colon**:

```
Router::add('/profile/:userId', [...]);
```

### Route finder

When using a route finder, it is your responsability to detect parameters, since you receive the accessed route as a string:

```
Router::addFinder(function($route) {
    // $route = '/profile/234' -> userId = 234
});
```

### Recover the passed parameter

The route **actions** for each method receive a second argument with an array containing the parameters in the URL:

```
Router::add('/api/profile/:userId', [

    'GET' => function($request, $params) {
    
        $userId = intval( $params['userId'] );
    
    }

]);
```
