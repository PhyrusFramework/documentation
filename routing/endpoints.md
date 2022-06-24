# Endpoints

A route must return an object (an array) defining the behavior of that route for each **method**:

```
// /back-end/routes/api/example/index.php
// https://mysite.com/api/example

return [
   'GET' => function($req) { },
   'POST' => function($req) { }
]
```

If this route is being accessed using any other method than the ones specified there (PUT, DELETE, etc) it will automatically return a **405 Method-Not-Allowed** error.

The method can output something directly or return an array and the framework will automatically convert it to JSON and display it:

```
return [
   'GET' => function($req) {
      
      $data = [
         'message' => 'Hello world'
      ];
      
      // Option 1:
      response_die('ok', JSON::stringify($data));
      
      // Option 2:
      return $data;
      
   }
]
```

### Using manual routing

When using manual routing, you can give the path to a file **returning** this object, or you can specify this object right there:

```
Router::add( '/my-route', Path::back() . '/whatever.php' );

// Or
Router::add( '/my-route', [
    'GET' => function($req) {
        // ...return $data;
    }
]);
```
