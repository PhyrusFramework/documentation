---
description: Change terms used by the framework
---

# Definitions

The framework uses a set of "**terms**" mostly for directories, such as "front-end", "back-end", "public", "routes", "code", "middlewares", etc.

These terms are not hardcoded along the code, but listed in an internal configuration file so they can be easily changed. However, when the framework starts, they are dumped into a memory object named **Definitions**. For example:

```
Definitions::get('back');  // returns 'back-end'
```

Using this class the terms can also be changed:

```
// Change the name of the directory "back-end" to "api"
Definitions::set('back', 'api');
```

From now on, and while that line is in the code, the folder /back-end is renamed to /api.

However, in order for this to work, definitions must be changed **before** launching the Router. So you should place it in the **/index.php** file in the **root folder**, right after the framework is loaded (composer) but before displaying the page:

```
<?php 
require(__DIR__.'/vendor/autoload.php');

* <-- HERE

// LAUNCH WEB
Router::launch();
```

Let's see a possible use:

### Different API versions

Imagine you have an API and you want to maintain multiple versions at the same time (as far as the framework version is the same).

You can use some factor to determine the user api version: an HTTP Header, URL path, etc. For example:

* Header api\_version: "v2"
* url:  mySite.com/api/v2/...

Then in your project you may have **multiple /back-end directories**, and set the one to be used depending on that parameter:

```
/back-end-v1
/back-end-v2
/back-end-v3
```

index.php:

```
<?php 
require(__DIR__.'/vendor/autoload.php');

///////////////////////////
// Use a header "api_version" to change the directory name
//
$req = RequestData::instance();
if ($req->headers->has('api-version')) {
    Definitions::set('back', 'back-end-' . $req->headers->{'api-version'});
}
//////////////////////////

// LAUNCH WEB
WebLoader::launch();
```

The advantatge of this strategy is that each api version would have not only different routes, but also different models and business logic.
