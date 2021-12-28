# CSS/SCSS

Phyrus also integrates SCSS and is automated so you don't have to worry about it. Any assets folder (/src/assets or specific controller page) may include scss files and they will be compiled (only when modified) and the browser will import the css version.

### Grid CSS

GridCSS is a CSS included in the framework to build responsive grids, similar to **Bootstrap** but slightly different.

{% hint style="info" %}
if you want to use Bootstrap instead, disable Grid CSS in the configuration file.
{% endhint %}

As in bootstrap, we have **containers, rows** and **columns:**

```
<div class="container">
    <div class="row">
        <div class="col">Content</div>
    </div>
</div>
```

In this case there are two ways of using columns:

```
<div class="row">
    <div class="col-2"></div>
    <div class="col-2"></div>
</div>

<div class="row">
    <div class="col-50-p"></div>
    <div class="col-50-p"></div>
</div>
```

The two examples above are equivalent, they will produce two columns, each occupying the 50% of the width.

When using a **col** class with the suffix **-p** we're using percentages. 25-p = 25%, 32-p = 32%.

When using a number, we're indicating **how many columns fit in a row**. (Or how many partitions there are). col-2 means two columns fit, so 1/2 each (50%). This example would be valid too:

```
<div class="row">
    <div class="col-4"></div>
    <div class="col-2"></div>
    <div class="col-4"></div>
</div>

<div class="row">
    <div class="col-25-p"></div>
    <div class="col-50-p"></div>
    <div class="col-25-p"></div>
</div>
```

### Container

As in Bootstrap, you can also use a **container** that will adapt to the screen width:

```
<div class="container">
    Content
</div>
```

#### Screen sizes

| Class prefix | Screen size                     |
| ------------ | ------------------------------- |
| col-lg       | Large: \[ 1200px - ? ]          |
| col-md       | Medium: \[ 991px - 1199px ]     |
| col-sm       | Small: \[ 768px - 990px ]       |
| col-xs       | Extra small: \[ 576px - 767px ] |
| col          | Default: \[ 0px - 575px ]       |

```
<div class="row">
    <div class="col-lg-4 col-md-3 col-sm-2 col-xs-1"></div>
</div>
```

This column will occupy:

* 25% width in large screens
* 33% width in medium screens
* 50% width in small screens
* 100% width in extra small screens

You don't need to specify all sizes, only the smaller one:

```
<div class="row">
    <div class="col-md-4 col-2"></div>
</div>
```

This column will occupy 25% in medium and large screens, and 50% in the rest of screens.
