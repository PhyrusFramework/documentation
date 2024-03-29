---
description: Get the path to any directory in the project
---

# Path

The Path class will give you the path, absolute or relative, to any directory in the project.

All methods receive a parameter true/false to indicate if you want the absolute(false) or relative(true) path:

```php
Path::root(); // absolute
Path::root(true); // relative
```

However, if you need to convert a path to relative or viceversa you can:

```php
$abs = Path::back();
$rel = Path::toRelative($abs);
$abs = Path::root() . $rel;

// Relative to /public
$rel = Path::toRelative('/public/images/x.png', true);
// /images/x.png
```

These are all the directories you can retrieve:

```php
Path::root();
Path::front();          //  /front-end
Path::back();           //  /back-end
Path::public();         //  /public
Path::framework();      //  /vendor/phyrus/framework
Path::tests();          //  /tests
Path::middlewares();    //  /back-end/middlewares
Path::routes();         //  /back-end/routes
Path::publicUploads();  //  /public/uploads
Path::privateUploads(); //  /uploads
```
