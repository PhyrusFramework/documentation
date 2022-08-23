# Event Listeners

EventListeners are used to leave functions prepared that will be executed later when an event triggers.

During the execution of your code you can add **actions** to an **event** (identified by a word), then this event can be triggered later:

```
EventListener::on( 'userRegistration', function($user) {
     sendMailToUser( $user);
});

EventListener::on( 'userRegistration', function($user) {
    sendNotificationToAdmins( $user);
});

// Later
EventListener::trigger( 'userRegistration', $user );
```

### Argument by reference

The argument of the event is passed by reference, that means that events have the hability to modifiy the argument and pass on the value:

```
EventListener::( 'addItems', function($list) {
    $list[] = 'A';
});

EventListener::( 'addItems', function($list) {
    $list[] = 'B';
});

// Later
$list = [];
EventListener::trigger( 'addItems', $list );
// Now $list = [ 'A', 'B' ]
```
