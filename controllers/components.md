---
description: Reusable components
---

# Components

Components are pieces of a website that you can reuse in multiple pages. A component may have multiple uses:

* Display blocks (HTML+CSS)
* Import libraries (PHP or JS-CSS)
* Front-end widgets (Vue components)
* Import common assets (css, js)

Components extend the **ComponentController** class:

```
// in /src/components/my-component
class MyComponent extends ComponentController
```

However, this class is a child of Controller, so it can do **completely the same** as a normal Controller. The difference is that the display method **must** receive a parameter:

```
function display( $params = [] ) { }
```

### Use components in pages

The point of components is precisely having **blocks** (html, php, js, css...) that won't be loaded always in every page, but only in those that need it.

For this, you must manually specify in which pages this component will be used. You can do this by defining the **components** property of a controller:

```
class PageController extends Controller {

    function init() {
        $this->components = ['my-component'];
        
        // Or also use a class instance
        $this->components = [new MyComponent()];
    }

}
```

When using a Component in your own project (located in /src/components), you can use **the name of the directory** ('my-component') and it will automatically import the PHP file and use that class.

However, if you are using an external component (for example from a Composer third package), you need to use **an instance of the component class**.

{% hint style="info" %}
As a ComponentController is also a normal Controller, a component can also define a **$components** array of its own, and then that component will load other components..
{% endhint %}

### PHP vs Vue Components

There are two very different ways to use components: **Front-End** and **Back-End** components. Both coexist in Phyrus.

One is using components tu build blocks with PHP (HTML) to be re-used in different pages. This will be rendered **server-side**, and finally the full page will be sent to the client.

The other is using components to declare **Vue** components, which are loaded by **Javascript** using the vue library on **client-side**.

### PHP Components

They work exactly like pages: there's a **controller.php**, a **view.php** and optionally a **vue** file:

```
component/component.controller.php
component/component.view.php
component/component.vue (Optional)
```

Then we insert that component in pages, by using the **component** method ot the **template filter**:

```
<div><?php component('MyComponent'); ?></div>
<div>[[cmp 'MyComponent']]</div>
```

In the end, it is as if the component was part of the page, with the advatage that it can be reused somewhere else. That block is just "**inserted**" into the page.

{% hint style="warning" %}
Beware that this insertion will be made **server-side** while rendering the page, and the client will receive all the page in one piece.
{% endhint %}

### Vue components

Vue components are front-end views that you can reuse in different pages. They are very useful because they seize the potential of **Vue**: data-binding and reactivity.

These may be very useful to build Javascript widgets (inputs, selectors, forms, buttons, sliders, etc).

When you create a Vue component, **there's not a view.php** file. Instead, you necessarily create a vue file, and the syntax changes a bit:

```
// component/component.vue
<template>
<div>
    This is my component's layout
</div>
</template>

<script>
new VueComponent('my-component', {
    // Vue properties (data, methods, created...)
});
</script>
```

The layout is defined in the same **vue** file. Then, to insert this component in a page, we use it as a HTML element:

```
<div>
    <my-component></my-component>
</div>
```

### Assets

In both cases indistinctly, a component directory may contain assets like any other normal controller. These assets **will only be loaded once**, regardless of how many times you repeat that block in the page.

This means that a page may display the same component three times (or none) and its assets (css, js) will be imported anyway and only once.

A ComponentController is just a normal controller, so it can do whatever a page controller does.
