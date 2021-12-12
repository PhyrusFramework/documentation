---
description: Controller resources
---

# Resources

A Controller is a **PHP file** in a folder, named like **\<anything>.controller.php** and containing a class that extends **Controller**.

When the framework loads a controller, its folder may contain many other optional things, like a **view** file, a **vue** controller, front-end **assets** or more **php**. If they exist, the framework will load them automatically, so you forget about imports.

### Controller View

A controller folder may contain a view file, which is a file named **the same as the controller**, but changing **.controller.php** for **.view.php**, for example:

```
/contact.controller.php
/contact.view.php
```

When you create a view file, you don't need to define the controller **display** method, it will be automatically loaded and displayed. However, if you needed to do it manually, the can do it like this:

```
function display() {
    // Your logic here
    
    $this->view();
    
    // Or pass parameters
    $this->view([...]);
}
```

Read more about **views and templating** in the next page.

### Controller assets and code

Inside a controller folder you can create sub-folders named **assets** and **code**, and they will work exactly as the ones in the main folder (/src). So the assets (js, css, scss) placed inside of /assets and the php files inside of /code will be automatically imported, **only when this controller is used**.

This is a huge feature, since you may have specific assets only for specific pages or components, instead of loading them everywhere.

### Vue controller

Phyrus integrates **Vue** (which is a Javascript framework that includes data-binding). You can read more in the specific section dedicated to Vue.

Each controller may include a Vue controller to be used along with the controller's view. To create a vue controller you only have to create a file named **xxx.vue** in the controller folder:

```
/contact.controller.php
/contact.view.php
/contact.vue
```

The vue file must contain this:

```
<script>
new VueController({
    // Here your vue properties (data, methods, created...)
});
</script>
```
