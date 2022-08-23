---
description: Receive HTTP requests as server
---

# Request Data

Everytime the website is accessed, you can instantiate an object of the class **RequestData** to get information about the request:

```php
$req = new RequestData();
// or
$req = RequestData::instance();

$m = $req->method();
if ($req->isMethod('GET'))
```

POST data can be accessed directly as properties of this object:

```php
$req = new RequestData();
$req->email
$req->username

if ($req->has('username')) {
    $username = $req->username;
}
```

If the constructor of RequestData gets **true** as parameter, it will also include **Query params**:

```php
$req = new RequestData(true);
// or
$req = RequestData::instance(true);

// /page?offset=34
$req->offset;
```

### Require method and data

When developing an API, you will usually need to require the client to use a specific method or to send some required data in the request. You could do it like this:

```php
if (!$req->isMethod('POST'))
   response_die('method-not-allowed');
   
if (!$req->has('email'))
    response_die('bad', 'Email missing');
```

But there is a simpler way:

```php
$req->requireMethod('POST');
$req->require('email');

$req->requireMethod('GET', 'POST');
$req->require('title', 'description');
```

**Require** will automatically return an error **400 Bad request** if any mandatory field is missing. **RequireMethod** will automatically return error **405 Method not allowed** if the request method is not accepted.

{% hint style="info" %}
In development mode, **require** will tell the client which field is missing. In production this information is hidden.

However, if you need to customize the response message, you can do it by checking the data yourself instead of using this method.
{% endhint %}

### Headers

The request headers can also be obtained through the RequestData object:

```php
$req = new RequestData();

if ($req->headers->has('some-header'))
    $req->headers->{'some-header'};
    
$req->headers->require('some-header');

$token = $req->Auth(); // Authorization header
$ct = $req->{'Content-Type'}

$req->require('some-header');
```

{% hint style="info" %}
Using Apache, if the AUTHORIZATION header is not working for you, make sure these lines are in your .htaccess file:

RewriteEngine On

RewriteCond %{HTTP:Authorization} ^(.\*)

RewriteRule _.\*_ - \[e=HTTP\_AUTHORIZATION:%1]
{% endhint %}

