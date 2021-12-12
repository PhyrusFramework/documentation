---
description: Page controller class
---

# Controller

A Controller is a class extending the **Controller** class:

```
class MyPageController extends Controller
```

You will never create a Controller **instance**, because the framework automatically imports it from any file named **xxx.controller.php**.

For example, when using manual routing, we can define this route:

```
Router::add('/contact', Path::src() . '/routes/contact' );
```

This means that, in the directory **/src/routes/contact** there should be a file named **\<whatever>.controller.php** (for example, contact.controller.php), defining a class like this:

```
class ContactPageController extends Controller { }
```

A folder containing a controller, may also contain many other **resources**, like assets (**css, scss, js**), a **view** or a **vue controller**. All of this will be automatically loaded, read about it later on.

### Controller lifecycle

You **must not** define a constructor for a Controller. Instead, a Controller consists of three methods: **init**, **prepare** and **display**:

```
class SomeController extends Controller {

    function init() {
       // Controller created
    }
    
    function prepare() {
       // Before display
    }
    
    function display() {
        // Display view
    }

}
```

The **init** method is the most similar thing to the constructor. It will be executed right after creating the controller instance, so use it as a constructor. It is executed **before** loading the controller resources.

The **prepare** method is executed **after** the controller resources have been loaded, but **before** displaying anything.

The **display** method is what renders the view of this controller.

{% hint style="info" %}
All these methods are optional.
{% endhint %}

The **display** method renders whatever is displayed in the browser when we access this Controller. By default it tries to load a **view.php** file, as explained in the next chapter. But you can try to override the display method and just display a message with **echo**:

```
class ContactPage extends Controller {

    function display() {
        echo 'Contact page';
    }

}
```
