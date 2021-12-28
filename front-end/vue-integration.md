---
description: How is Vue integrated into Phyrus
---

# Vue integration

How is Vue integrated with Phyrus? How do we use Vue in a Phyrus project?

Vue works with **.vue** files.

{% hint style="info" %}
For Visual Studio Code we can install the official Vue extension to work with these files.
{% endhint %}

Vue files must be located into a folder of a controller, along with the controller:

```
/example/example.controller.php
/example/example.vue
```

Then we can use two different types of vue objects: **VueController** vs **VueComponent**.

{% hint style="info" %}
This concepts belong to Phyrus, don't search them in the Vue documentation.
{% endhint %}

In a **VueController** the view (HTML) is server-side rendered by a PHP file. So normally we will use it for pages and huge components (like website header and footer).

In a **VueComponent** the view (HTML) is rendered client-side by javascript, so we will use it to build widgets: calendar, language switcher, buttons, dropdowns, file pickers...

Furthermore, VueComponents can be used in HTML as **custom tags** \<my-component>

### VueController

In the Controller folder you will place three files: the **controller** (PHP), the **view** (PHP), and the **vue** controller (JS):

```
/pages/contact-page/contact-page.controller.php
/pages/contact-page/contact-page.view.php
/pages/contact-page/contact-page.vue
```

The view (HTML) will be placed in the **.view.php** file. There we can freely use PHP logic, which will be rendered server-side.

Once sent to the client (browser), Javascript will use the vue controller. In the **vue file** we need to define a **VueController**:

```
// contact-page.vue
<script>
new VueController({
    data: { ... },
    methods: { ... },
    created: { ... }
});
</script>
```

If this is used in a **page**, we don't need anything else. This VueController will be used when we access a page.

If this is a **Phyrus component**, remember that you need to include that component in the page controller, and then insert the component in the view:

```
// page.controller.php
function init() {
    $this->components = ['my-component'];
}

// page.view.php
<div>
    [[cmp 'MyComponentClass']]
</div>
```

### Vue component

In a VueComponent we will not use a **.view.php** file, since the view is not server-side rendered. Instead, it needs to be declared inside the **.vue** file, along with a **VueComponent** class object:

```
// /components/form-field/form-field.vue
<template>
    <div class="form-field">
        <label>{{ label }}</label>
        <input v-model="inputValue">
    </div>
</template>

<script>
new VueComponent('form-field', {
    props: ['label'],
    
    data: {
        inputValue: ''
    }
});
</script>
```

As you can see, VueComponent receives a first string parameter, which is the name of the **HTML tag** we'll use to insert it in a page:

```
<div>
    <form-field label="Username"></form-field>
</div>
```

### Phyrus components + Vue components

Important: **a Phyrus component is not necessarily a VueComponent**.

In our Phyrus project there is the folder **/src/components**. A component is a block (HTML|CSS|JS|PHP) that we can reuse in multiple pages. However, we can use components to define VueControllers, VueComponents or none at all (for instance only a CSS component, or a PHP component).

Let's imagine two Phyrus components: **HeaderMenu** and **CalendarWidget**.

**HeaderMenu** will be the top header menu of the website, it will be a common part to all pages. In this case it is a dynamic block for which we need server-side rendering (PHP logic). So we will use a **VueController**:

```
/components/header-menu/header-menu.controller.php
                       /header-menu.view.php
                       /header-menu.vue
                       
new VueController({ ... });
```

The view will be rendered in PHP. Client-side logic (JS) will be placed in the vue file. And we will insert the menu in the page (or in a middleware) like this:

```
[[cmp 'HeaderMenu']]
<div id="page-content">
    [[ $controller->display() ]]
</div>
```

Now let's imagine the second case, **Calendar widget**. Now we don't need the view to be rendered by PHP, instead we want a usable widget that can be integrated like this:

```
<div>
    <calendar-widget initial-month="03/2022"></calendar-widget>
</div>
```

In this case we won't use a VueController, instead we will define a **VueComponent**, and the view will be **included in the vue file**:

```
/components/calendar-widget/calendar.vue
<template>
    <div class="calendar">
        ...
    </div>
</template>
<script>
new VueComponent('calendar-widget', {
    props: ['initial-date'],
    ...
});
</script>
```

**Conclusion**: which methodology to use is up to you.
