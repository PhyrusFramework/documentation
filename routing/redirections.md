---
description: Redirect from a page to another
---

# Redirections

Using the **Router** class, you can easily make a 301 Redirection:

```
Router::redirectTo('/');
```

However, this redirection must be executed before displaying anything in the website, the right place would be the **init** or **prepare** methods in a Controller.

Another option is making a Front-End redirection using Javascript. You can do that from PHP executing:

```
Javascript::redirectTo('/');
```

The right place for this would be the **display** method in the controller.
