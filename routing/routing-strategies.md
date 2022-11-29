---
description: You can choose how to route your pages
---

# Routing methods

Routing means to decide what code must be executed depending on the URL route that is being accessed. Phyrus gives you **three** different ways to decide that:

* CRUD (recommended)
* Automatic routing
* Manual routing

### CRUD

The recommended way to create an API is the CRUD object. It is a bit more complex, so it deserves its own page. Read [the next chapter](crud.md) about it.

### Automatic routing

Doing something similar to Nuxt with page routing, Phyrus can automatically use your directory structure to guess the URL. Inside the **/back-end** directory you can use a directory named **/routes** to create your routes using the directory structure. Example

```
/back-end/routes/contact/index.php
mysite.com/contact

/back-end/routes/api/users/_id/index.php
mysite.com/api/users/23
```

### Manual routing

Manual Routing works like in most of other frameworks, you need to manually write the route and what it does. **Only that here you can use either the path to a file, or the action directly**:

<pre class="language-php"><code class="lang-php"><strong>// file
</strong><strong>Router::add('/api/create', Path::back() . '/my-routes/create.php' );
</strong>
// action
Router::add('/api/create', [
   'GET' => function($req) { ... }
]);</code></pre>

### Redirections

Using the **Router** class, you can easily make a 301 Redirection:

```php
Router::redirectTo('/');
```

### The Route object

Both **Automatic** or **Manual** routing will need to return a **Route object**. This is an object with each one of the supported methods for that route, and what it does. Example:

```php
// /back-end/routes/api/users/_id/index.php

return [
    'GET' => function($req, $params) {
        // Get the user
        return User::findID($params->id);
    },
    
    'PUT' => function($req, $params) {
        // Edit user...
    }
];
```

Same with Manual routing:

```php
Router::add( '/api/users/:id', [
    'GET' => function($req, $params) {
        // ...
    },
    'PUT' => function($req, $params) {
        // ...
    })
]);
```

If a route is accessed with a method that is not supported, it will return a **405 error, Method Not Allowed**.

