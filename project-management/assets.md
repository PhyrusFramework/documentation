---
description: Add front assets to the page
---

# Assets

The assets page lets you access the project assets and also add them to the page (js, css, scss, images, etc).

```
// Get routes

$src = Assets::image('logo.png');
// returns /src/assets/images/logo.png

$src = Assets::front('myFont.ttf');
// returns /src/assets/fonts/myFont.ttf

Assets::css('style.css');  /src/assets/css/style.css
Assets::js('script.js');   /src/assets/js/script.js
```

Add assets to the page:

```
Assets::setFavicon( Assets::image('logo.ico') );

Assets::include_css( Path::toRelative($file) );
Assets::include_js( Path::toRelative($file), $inFooter?);
Assets::include_js( 'https://some.library.js', $inFooter? );
```

You can also directly import all assets under a directory:

```
Assets::css_in($directory, $recursive?);
Assets::js_in($directory, $recursive?);
Assets::scss_in($directory, $recursive?);

// Any kind of asset
Assets::assets_in($directory, $recursive?);
```

Notice that any of these lines is equivalent to doing something like this:

```
Head::add(function(){ ?>
    <script src="..."></script>
<?php );
```

### Avoid browser caching

Phyrus includes a method to avoid this annoying problem when you make a change but due to browser's cache users can't see the change at the moment.

If you check your configuration file, you will see this parameter:

```
"assets": {
    "disable-cache-after-modification-for-x-hours": 1,
```

This will automatically add a random parameter to the URL to each asset **modified in less than one hour** ago:

```
<link rel="stylesheet" src="/web/assets/css/style.css?cache=a5G3t">
```

You can change the amount of hours that cache is disabled, or **disable** this feature by setting it to **zero**.
