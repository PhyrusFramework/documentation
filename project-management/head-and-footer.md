---
description: Add content to the <head> and footer
---

# Head\&Footer

As you have noticed, Phyrus builds the HTML wrapper structure for you. That means that you don't need to build the HTML page from scratch, you only worry about the current page:

```
<html>
   <head>...</head>
   <body>
      * <-- YOUR CONTROLLER DISPLAY
   </body>
</html>
```

This doesn't mean that you can't add custom lines to this structure, for that Phyrus has the hook classes **Head** and **Footer**. You can use them to add lines in those blocks:

```
Head::add('some line');
Head::add(function() { ?>
    <script src="..."></script>
    <link rel="stylesheet" href="...">
<?php });

Footer::add('some line');
Footer::add(function() { ?>
    <script src="..."></script>
<?php });
```

### Controlling order with priorities

By default the lines will be printed in the same order you add them.

When printing the page, these lines will be ordered by its **priority** property. By default all have a priority of 10.

However, you can force the order by adding a second parameter as the priority:

```
Head::add('line1'); // priority 10
Head::add('line2', 1); // priority 1 (>)
Head::add('line3', 20); // priority 20
```

The order of these lines in the head will be:

* line 2
* line 1
* line 3

