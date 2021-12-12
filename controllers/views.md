---
description: Phyrus views and templating
---

# Views

Phyrus has a **templating** system to help you work with layouts and PHP. **Any php** file can be a view, and the you can load it with:

```
view($file);

// Or pass parameters
view($file, [
   'title' => 'This is the title'
]);
```

A view file uses double square brackets **\[\[ ]]** to open and close PHP tags:

```
<div>
   [[ $title ]]
</div>
```

The opening brackets may include a keyword to express a specific PHP functionality, that's a **filter**:

```
[[if !Auth::loggedIn() ]]
    <div>Register to purchase!</div>
    
[[elseif !empty($products) ]]

    <div>There are [[size $products]] products</div>

    [[run $i = 0]]
    [[foreach $products as $product]]
         [[run $i++]]
         <h3>Product nº[[$i]]</h3>
         <div>[[$product->name]] - [[$product->price]]</div>
    [[/]]

[[else]]
    <div>Empty cart</div>
[[/]]
```

### Controller views

Controllers use views automatically. When a controller does not include a **display** method, it will try to find a view file by default. In this case, to identify the view file automatically, the name **must** be the same as the controller but ended with **view.php**:

```
page.controller.php
page.view.php
```

Controllers have a method named "**view**" to load its view, which works exactly like the generic function, except that we don't need to pass a path to the view file (it's supposed to be the one with the controller name, as shown above).

```
function display() {
    $this->view([
        'products' => Products::get();
    ]);
}
```

### Collision with Vue

Phyrus' templating uses square brackets **\[\[ ]]** instead of curly brackets **{{ }}** because those are reserved to Vue.

Vue also has its own templating system, so Vue's templating and Phyrus' templating coexist in the same framework and in the same view files. This means that a view file may contain **both systems**:

```
<div>
    <h1>[[ $title ]]</h1>
    <div v-for="product of products">
        <div>{{product.name}}: {{product.price}}</div>
    </div>
</div>
```

The difference is that square brackets will be executed as **PHP in server-side**, and curly brackets will be executed as **Javascript in client-side**.

So, which one to use is up to you, depending on the architecture of your project. But you must know which one to use in each case. Ones will be executed in the server **before** the website is sent to the user, and the others will be executed by their browser.

### Create your own filters

You can extend and customize the templating system by creating your own templating filters, which will make the development of layouts much easier for you. See an example:

```
Template::addFilter('lower', function($content) {
    // Return the PHP code to execute
    return "strtolower($content)";
});
```

Then in the view:

```
<div>[[lower 'This a TEXT I want in lowercase']]</div>
```

### Filter reference

| Filter   | Description                              | Example                                                               |
| -------- | ---------------------------------------- | --------------------------------------------------------------------- |
| (empty)  | Equals to echo                           | \[\[$var]]                                                            |
| run      | Executes without display                 | \[\[run $i = 0]]                                                      |
| img      | Path to /src/assets/images/              | \<img src="\[\[img 'logo.png']]">                                     |
| size     | Displays the size of something           | \<div>\[\[size $arr]]\</div>                                          |
| if       | If condition                             | \[\[if $bool]] ... \[\[/]]                                            |
| /        | Close any block                          | \[\[/]]                                                               |
| while    | While loop                               | \[\[while $cond]] ... \[\[/]]                                         |
| for      | For loop                                 | \[\[for $i=0; $i<$n; $i++]]                                           |
| forn     | For from 0 to n                          | \[\[forn 10]] \<div>\[\[$index]]\</div> \[\[/]]                       |
| foreach  | Iterate array                            | \[\[foreach $arr as $k => $v]] ... \[\[/]]                            |
| else     | Else                                     | \[\[if $cond]] ... \[\[else]] ... \[\[/]]                             |
| elseif   | Else if                                  | \[\[if $cond]] ... \[\[elseif $cond2]] ... \[\[/]]                    |
| func     | Create function                          | <p>[[func addNumbers($x, $y)]]<br>[[run return $x + $y]]<br>[[/]]</p> |
| view     | Load another view file                   | \[\[view $file]]                                                      |
| t        | Translate using phyrus' translate system | \[\[t 'abc.def']]                                                     |
| empty    | If empty                                 | \[\[empty $arr]] .... \[\[/]]                                         |
| notempty | If not empty                             | \[\[notempty $arr]] ... \[\[/]]                                       |
| cmp      | Display a component view                 | \[\[cmp 'ClassName']]                                                 |

