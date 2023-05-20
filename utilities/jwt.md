---
description: JSON Web Tokens
---

# JWT

**JWT (JSON Web Tokens)** is a common encryption system widely used for client authentication and communication between server and client. A token (string) is generated using a private key and may contain encrypted data.

First you need to create a **JWT** object using the private key:

```php
new JWT( $key, $age? = 3600, $algorithm? = 'HS256');

$jwt = new JWT( 'key' );
$jwt = new JWT( 'key',  10000 );
```

A JWT Token **expires**, when the token expires it's no longer usable. By default it will expire in an hour, but that can be configured with the second parameter of the constructor.

Now this object can be used to decode existing tokens or generate new tokens:

```php
// generate
$token = $jwt->encode([
    'user_id' => 23
]);

// read
$payout = $jwt->decode($token);
$payout['user_id'];
```

You can check if the token has expired:

```php
if ($jwt->isExpired($token)) {
   response_die('unauthorized', 'Your token has expired');
}
```
