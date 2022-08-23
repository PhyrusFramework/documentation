---
description: Manage cookies and session
---

# Cookies & Session

Cookies and Sessions can be controlled with the classes **Cookie** and **SESSION**. They work almost identical, working with static methods:

```php
if (!Cookie::has('key'))
   Cookie::set('key', 'value');
Cookie::get('key', $default?);
Cookie::destroy( 'key' );

if (!SESSION::has('key'))
    SESSION::set( 'key', 'value' );
SESSION::get('key', $default?);
SESSION::destroy('key');
```

### Expiration time

In the case of Cookies expiration time can be controlled by using a third parameter **in days**:

```php
Cookie::set( 'key', 'value', 2);  // 2 days
Cookie::set( 'key', 'value', 0.5);  // 12 hours
Cookie::set( 'key', 'value', 1/24); // 1 hour
```

If you don't want to manually set the time every time, you can set the default expiration time at the beginning:

```
Cookie::$expiration = 10;  // set to 10 days
// Default is 365
```

### **Sessions**

The session **is started automatically** when setting a value if it wasn't, so you don't have to think about that. You can check the ID or the status:

```php
SESSION::set('a', 123);hphhhh

$id = SESSION::ID();
$status = SESSION::status();   // active, disabled, none

if (!SESSION::isStarted()) {
    SESSION::start();
}
```
