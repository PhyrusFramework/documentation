---
description: Receive HTTP requests as server
---

# As server

Everytime the website is accessed, we can instantiate an object of the class **RequestData** to get information about the request:

```
$req = new RequestData();
// or
$req = RequestData::instance();

$req->method();
if ($req->isMethod('GET'))
```

We can get the POST data directly as properties of the request:

```
$req = new RequestData();
$req->email
$req->username

if ($req->has('username')) {
    $username = $req->username;
}

// To get also URL parameters pass true to the constructor:
// /page?offset=34
$req = new RequestData(true);
$req->offset;
```

### Require method and data

When developing an API, you will usually want to require the request to use a specific method or to receive mandatory data, you could do it like this:

```
if (!$req->isMethod('POST'))
   response_die('method-not-allowed');
   
if (!$req->has('email'))
    response_die('bad', 'Email missing');
```

But there is a simpler way:

```
$req->requireMethod('POST');
$req->require('email');

$req->requireMethod('GET', 'POST');
$req->require('title', 'description');
```

**Require** will automatically return an error **400 Bad request** if any mandatory field is missing. **RequireMethod** will automatically return error **405 Method not allowed** if the request method is not accepted.

### Headers

The request headers can be obtained through the **headers** object of the RequestData:

```
$req = new RequestData();

if ($req->headers->has('some-header'))
    $req->headers->{'some-header'};
    
$req->headers->require('some-header');

$token = $req->Auth(); // Authorization header
$cp = $req->{'Content-Type'}

$req->require('some-header');
```

{% hint style="info" %}
Using Apache, if the AUTHORIZATION header is not working for you, make sure these lines are in your .htaccess file:

RewriteEngine On

RewriteCond %{HTTP:Authorization} ^(.\*)

RewriteRule _.\*_ - \[e=HTTP\_AUTHORIZATION:%1]
{% endhint %}

