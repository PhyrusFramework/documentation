---
description: Get the path to any directory in the project
---

# Path

The Path class will give you the path, absolute or relative, to any directory in the project.

All methods receive a parameter true/false to indicate if you want the absolute(false) or relative(true) path:

```
Path::src(); // absolute
Path::src(true); // relative
```

However, if you need to convert a path to relative or viceversa you can:

```
$abs = Path::assets();
$rel = Path::toRelative($abs);
$abs = Path::root() . $rel;
```

These are all the directories you can retrieve:

```
Path::root();
Path::project();    //  same as root
Path::framework();  //  /framework
Path::src();        //  /src
Path::assets();     //  /src/assets
Path::js();         //  /src/assets/js
Path::css();        //  /src/assets/css
Path::images();     //  /src/assets/images
Path::fonts();      //  /src/assets/fonts
Path::code();       //  /src/code
Path::components(); //  /src/components
Path::middlewares();//  /src/middlewares
Path::pages();      //  /src/pages
```
