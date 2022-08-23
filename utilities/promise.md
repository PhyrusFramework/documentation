---
description: Promise PHP
---

# Promise

**Promises** are a native feature in **Javascript**. A Promise runs a code and this code can end in success or failure:

```php
doSomething()
    ->then(function() {
        echo "Success!"
    })
    ->catch(function() {
        echo "Failed!";
    });
```

Some Phyrus features return a Promise, like HTTP Requests.

It works quite similar to **Javascript**:

```php
function example() {
    return new Promise(function($resolve, $reject) {
        // ... do something        

        if ($success)
            $resolve($value);
        else
            $reject('Something failed');
    });
}

example()
    ->then(function($value) {
        // success
    })
    ->catch(function($err) {
        // error
    })
    ->finally(function() {
        // anyway
    });
```

{% hint style="warning" %}
Remember, to use external variables in an anonymous function you need to add **use($variable)**:
{% endhint %}

```php
$name = 'some value';

example()
    ->then(function() use ($name) {
        echo "$name can be used now";
    });
```

### Use synchronously

The hassle of using promises is that you need to use **callback functions** (then, catch). Sometimes that can be a problem, so instead you can obtain the result directly:

```php
$promise = doSomething();

if ($promise->isSuccess()) {
    return $promise->getResponse();
}
else {
    ApiResponse::error( $promise->getError() );
}
```
