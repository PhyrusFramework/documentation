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
