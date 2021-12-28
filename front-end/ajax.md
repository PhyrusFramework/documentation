---
description: Asynchronous JavaScript
---

# AJAX

Although AJAX stands for (**Asynchronous JavaScript and XML**), nowadays it usually refers to asynchronous http requests made by the client (Javascript) to the server (in this case, PHP) to obtain data once the page is loaded.

We can see ajax requests, for instance, when youtube loads. The page loads first, and later, the videos appear. It is possible that you are familiar with ajax working with jQuery.

Phyrus makes easier for you to send asynchronous requests. First in PHP you need to define an ajax method. This method will automatically receive a **RequestData** object as parameter.

```
Ajax::add('doSomething', function($req) {
    $req->requireMethod('POST');
    ...
});
```

Then, the website can use this method from javascript.

```
// Javascript
Ajax.post('doSomething', data)
.then(response => { });
```

### Request response

To return a response, you can **echo** something or anything returned will be **converted to JSON**:

```
Ajax::add('htmlExample', function($req) {
    echo '<div>some HTML</div>';
});
Ajax::add('jsonExample', function($req) {
    return [
        'message' => 'works!'
    ];
});
```

### Ajax in Controllers

There's still a simpler way to make Ajax methods. You can use methods in a Controller as ajax callable methods:

```
// PHP
class MyController extends Controller {
    function init() {
        $this->ajax = [
            'doSomething'
        ]
    }
    
    function doSomething($req) { }
}

// Javascript
Ajax.post('doSomething', data);
```
