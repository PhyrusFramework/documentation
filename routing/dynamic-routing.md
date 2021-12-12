---
description: Use dynamic parameters in the URL for routing
---

# Dynamic routing

Dynamic routing refers to using dynamic variables in the route as parameters, such as:

* /profile/:userId
* /project/:projectId/members

All routing strategies allow this feature.

### Automatic routing

With automatic routing you only have to start the directory name with an underscore to indicate that it is a parameter. For the previous examples would be:

* /src/pages/profile/pages/\_userId
* /src/pages/project/pages/\_projectId/pages/members

Later, you can retrieve this parameter in the Controller, read about controllers later.

### Manual routing

In the case of manual routing, parameters are specified with a colon:

```
Router::add('/profile/:userId', Path::src() . '/routes/profile');
Router::add('/project/:projectId/members', Path::src() . '/routes/project-members');
```

### Route finder

When using a route finder, it is your responsability to detect parameters, since you receive the accessed route directly:

```
Router::addFinder(function($route) {
    // $route = '/profile/234' -> userId = 234
});
```
