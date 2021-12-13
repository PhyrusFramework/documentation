---
description: Using Controllers to make pages
---

# Pages

Controllers have multiple uses: **pages**, **components** or **middlewares**. The most obvious use is to create pages using the Routing system. As we've already seen we can create a page controller, for example, using Automatic Routing:

```
/src/pages/about/about.controller.php
```

This Controller will "control" the view and resources for the path https://mysite.com/about.

With the controller **folder** we may have a view and specific assets or code for this page. However, when we develop a website page, there are more configurations we need to make.

### Page metadata

The controller has a **meta** property we can use to define the basic metadata properties:

```
class Page extends Controller {

    function init() {
        $this->meta->title = $title;
        $this->meta->charset = 'UTF-8'; // Default
        $this->meta->description = $description;
        $this->meta->keywords = '';
        $this->meta->author = 'me';
        $this->meta->viewport = 'width=device-width, initial-scale=1'; // default
    }

}
```

You can also execute this lines in the **prepare** method.

### Raw output

By default, any page will be a HTML page with \<head> and \<body>. That's normal when you develop a website.

However, if you're developing something else, like an API, you won't want this HTML wrapper. Then you need a **raw** controller, and for that you can set the raw property of the controller to true:

```
function init() {
    $this->raw = true;
}

function display() {
    echo JSON::stringify([...]);
}
```

### Include assets

We may also need to add front-end assets (js, css).

{% hint style="info" %}
Remember that a Controller folder may already include an **assets** folder, and all assets inside will be automatically imported, so you don't need to do this.
{% endhint %}

For example, you could use this to import a third-party Javascript library, only for this page.

```
class Page extends Controller {

    function init() {
        Assets::include_css($src);
        Assets::include_js($src);
        Assets::include_js($src, true); // Footer
        
        // Detect files automatically
        Assets::css_in($directory, $recursive);
        Assets::js_in($directory, $recursive);
        Assets::assets_in($directory, $recursive);
    }

}
```

### Adding lines to the Head for Footer

Finally, we may also need to add custom lines to the page \<head> or footer elements. For this, we can use the **Head** and **Footer** classes:

```
class Page extends Controller {

    function init() {
        
        Head::add('some line');
        // Or use a function
        Head::add(function(){ ?>
            <meta name="description" content="Description">
        <?php });
        
        Footer::add('line');
        Footer::add(function(){ ?>
            <script>
            // Do something
            </script>
        <?php });
        
    }

}
```

{% hint style="info" %}
These methods **do not need** to be used inside a Controller. We can also use them inside a file in /src/code to execute them for any page of our website.
{% endhint %}

If you need to force the order of these lines, you can also add a priority as second parameter:

```
Head::add('line');    // Priority 10
Head::add('line', 3); // Priority 3, goes first
```

