# Request & Params

As you may have noticed, the function of a route always received two parameters: **$req** and **$params**.

```php
Router::add('/api/users/:id', [
    'POST' => function($req, $params) {
        // ...
    }
]);
```

The first object is a **RequestData** object, explained later in the documentation. But basically is the one that contains the both the POST data and also query params, and is used to obtained the data, uploaded files, check headers, etc.

The second parameter **$params** is just an object containing **route parameters**, this means dynamic values in the route (not query params).

```php
Router::add('/api/users/:userId/projects/:projectId', [
    'PUT' => function($req, $params) {
        $uid = intval($params->userId);
        $pid = intval($params->projectId);
    }
]);
```
