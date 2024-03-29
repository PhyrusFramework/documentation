---
description: Translate your application
---

# Translations

Phyrus includes a translation system to manage translations and languages in the project. The translations can be used both in the back-end and front-end. So the same translations can be used for the website, to send emails, render PDFs, send notifications, etc.

When translations are used for the first time, a new YAML configuration file will appear in your configuration directory. If you don't have that configuration file yet, run this somewhere:

```php
new Translate();
```

Now if you check your configurations, there's a new YAML with these settings:

```php
use_cookies: true,
default_language: "en",
supported_languages: ["en"],
inherit: [],
directory: "/translations",
```

| Configuration        | Description                                           |
| -------------------- | ----------------------------------------------------- |
| use\_cookies         | Use cookies to store the current language of the user |
| default\_language    | Language to be used by default                        |
| supported\_languages | Languages you want to support                         |
| inherit              | **explained next**                                    |
| directory            | Folder containing translations                        |

To translate, first you need to create a **Translate** object using the desired language:

```php
$lang = Translate::use('en');

// Then, get the translation
$text = $lang->get('my.translation');
```

If the language is not specified, it will use the **default language**. However, you can also detect the user's language automatically:

```php
$langCode = Translate::browserLanguage();
$lang = Translate::use($langCode);
```

However the user language could not be supported by your application, so you can also use this method:

```php
$langCode = Translate::browserSupportedLanguage();
```

In this case, you will get the browser language **if supported**. If not, the default language will be used. A faster way to get the language for the current user is:

```php
$lang = Translate::use('user');
$lang->get('my.translation');
```

### Inheritance

In some countries, multiples languages are spoken. So a speaker from one of those languages will probably understand the others.&#x20;

For example, in Ukraine both Ukrainian and Russian are spoken, so if you support russian but not ukrainian, and your default language is english, your ukrainian users should see the website in russian, not english.

Another example, Catalan and Basque are other languages spoken in Spain, so their speakers should see the website in spanish, not english.

To solve this problem, there is a configuration named **inherit** used to "**redirect**" unsupported languages to other supported languages:

```
default_language: "en"
supported_languages: ["en", "es", "ru"]
inherit:
   uk: "ru"
   ca: "es"
```

With this configuration, when using **Translate::browserSupportedLanguage()** or **Translate::instance('user')** an ukrainian user would get russian, not english.

### Change the language

The user's language can be changed by running this:

```php
Translate::setLanguage('fr');
```

**If cookies are enabled**, this will create a new cookie to remember the language chosen by the user. Then, this is the language obtained when running:

```php
Translate::use('user');
```

This line will use the language chosen by the user (cookie), and if the cookie does not exist, then the browser supported language, and finally the default language.

**If cookies are not enabled**, the value will be stored in the session and lost soon.

### Parameters

Translations can carry dynamic parameters:

```php
// JSON
"product": {
    "price": "The price is {{price}}$"
}

// PHP
$t->get('product.price', [ 'price' => 34.99 ]);
```

### Dynamic translations

Translations are stored as JSON files in your translations directory. However, you might want to load translations dynamically on runtime.

To do it, you need to **merge** an array to the current translations:

```php
Translate::use('en')->merge([
    'pages' => [
        'checkout' => [
            'purchase' => 'Purchase'
        ]
    ]
]);
```

If the translation already existed, it will be overwritten.

{% hint style="info" %}
**Merge** only needs to be run once, from then on, the modification will be available everywhere.
{% endhint %}
