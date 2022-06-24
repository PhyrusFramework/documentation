---
description: Get the path to any directory in the project
---

# Path

The Path class will give you the path, absolute or relative, to any directory in the project.

All methods receive a parameter true/false to indicate if you want the absolute(false) or relative(true) path:

```
Path::root(); // absolute
Path::root(true); // relative
```

However, if you need to convert a path to relative or viceversa you can:

```
$abs = Path::back();
$rel = Path::toRelative($abs);
$abs = Path::root() . $rel;

// Relative to /public
$rel = Path::toRelative('/public/images/x.png', true);
// /images/x.png
```

These are all the directories you can retrieve:

```
Path::root();
Path::front();      //  /front-end
Path::back();       //  /back-end
Path::public();     //  /public
Path::framework();  //  /vendor/phyrus/framework
Path::tests();      //  /tests
Path::code();       //  /back-end/code
Path::middlewares();//  /back-end/middlewares
Path::routes();     //  /back-end/routes
```
