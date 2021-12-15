---
description: Change terms used by the framework
---

# Definitions

The framework uses a set of "**terms**" mostly for directories, such as "src", "$homepage", "$404", "pages", "components", "middlewares".

These terms are not hardcoded but defined in an internal configuration file. However, when the framework starts, they are loaded into a class named **Definitions**. For example:

```
Definitions::get('src');  // returns 'src'
```

Using this class we can also change these terms:

```
Definitions::set('src', 'www');

Path::src(); // returns 'www'
```

From now on and while that line is in the code, the folder /src must be renamed to /www.

However, in order for this to work, Definitions must be changed **before** starting the routing. Sou you should place it in the file **/index.php**, right after the framework is loaded (composer) but before displaying the page:

```
<?php 
require(__DIR__.'/vendor/autoload.php');

* <-- HERE

// LAUNCH WEB
WebLoader::launch();
```

Let's see a possible utility:

### Different project versions

Imagine you have an API, or a website. And you want to mantain multiple versions at the same time (as far as the framework version is the same).

You can use some factor to determine the version to display: HTTP Header, URL path, etc. For example:

* Header api\_version: "v2"
* url:  mySite.com/v2/...

Then in your project you can have **multiple src folders**, and set the one to be used depending on that parameter:

```
// Project directory:
/index.php
/framework
/srcv1
/srcv2
```

index.php:

```
<?php 
require(__DIR__.'/vendor/autoload.php');

// Header
$v = getHeader('api-version');
// URL
$path = URL::path();
$first = sizeof($path) > 0 ? $path[0] : '';
$v = $first == 'v2' ? 'v2' : 'v1';

// Change src folder
Definitions::set('src', "src$v");

// LAUNCH WEB
WebLoader::launch();
```
