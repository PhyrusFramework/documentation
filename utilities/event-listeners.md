# Event Listeners

Event listeners are used to define actions that will perhaps be executed later if the event triggers. During the execution of your code you can add **actions** to an **event** (identified by a word), then this event can be triggered later.

For instance. Imagine a shop. When the customer purchases a product, he has to receive a mail with the invoice.

```php
// Soon in the code
EventListener::on( 'purchase', function($data) {
     sendInvoiceMail($data);
});

// Later somewhere else
EventListener::trigger( 'purchase', [
     'user' => $user,
     'product' => $product
]);
```

This is also very useful to create **hooks.** That is spaces where you or other developers can insert code from outside:

```php
// Imagina a composer package doing this:
EventListener::trigger('Library:beforeLoad');
// --> load my library
EventListener::trigger('Library:beforeDisplay');
// --> display();

// Now the developer using this package can insert his own code in the middle:
EventListener::on('Library:beforeDisplay', function() {
    // Do something
});
```

### Argument by reference

The argument of the event is passed by reference, that means that events have the ability to modifiy the argument and pass on the value:

```php
EventListener::( 'addItems', function($list) {
    $list[] = 'A';
});

EventListener::( 'addItems', function($list) {
    $list[] = 'B';
});

$list = [];
EventListener::trigger( 'addItems', $list );
// Now $list = [ 'A', 'B' ]
```
