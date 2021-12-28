---
description: Integrate a google font in your website fast and easy
---

# Google fonts

The Google Fonts class lets you easily apply a Google font to your website in just a few lines. The right location to place this code would be in any file inside the /code folder, since php files there are imported for the whole website.

```
GoogleFonts::use('Roboto');
```

With a second parameter you can customize the font:

```
GoogleFonts::use('Roboto', [
    'weight' => '300,400,700',
    'style' => 'sans-serif',
    'selector' => '*'
]);
```

Optionally you can specify the default weight and size.

```
GoogleFonts::use('Roboto', [
    'default_weight' => '300',
    'default_size' => '13px'
]);
```
