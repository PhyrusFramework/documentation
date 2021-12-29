---
description: Promise PHP
---

# Promise

Promises here work exactly like Javascript promises:

```
function example() {
    return new Promise(function($resolve, $reject) {
        // do something
        $resolve($value);
    });
}

example()
    ->then(function($value) {
        // ...
    })
    ->catch(function($err) {
        // ...
    })
    ->finally(function() {
        // ...
    });
```

{% hint style="warning" %}
Remember, to use external variables in an anonymous function you need add **use($variable)**:
{% endhint %}

```
$name = 'some value';

example()
    ->then(function() use ($name) {
        echo "$name can be used now";
    });
```
