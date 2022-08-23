---
description: Manage cookies and session
---

# Cookies & Session

Cookies and Sessions can be controlled through the classes **Cookie** and **SESSION**. They work almost identical, working with static methods:

```
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

In the case of Cookies you can control the Age by using a third parameter **in days**:

```
Cookie::set( 'key', 'value', 2);  // 2 days
Cookie::set( 'key', 'value', 0.5);  // 12 hours
Cookie::set( 'key', 'value', 1/24); // 1 hour
```

If you don't want to manually set the time in every call, you can set the static default expiration time:

```
Cookie::$expiration = 10;
// Default: 365
```

### **Sessions**

The session **is started automatically** when setting a value if it wasn't, so you don't have to think about that. You can check the ID or the status:

```
$id = SESSION::ID();
$status = SESSION::status();   // active, disabled, none

if (!SESSION::isStarted()) {
    SESSION::start();
}
```
