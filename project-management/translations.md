---
description: Translate your application
---

# Translations

Phyrus includes a system to manage translations and languages through the **Translate** class.&#x20;

When the class is used for the first time, it gets **get installed** by adding new configurations and creating the directory and **json files** for each language (by default only english). Just run:

```
new Translate();
```

Then, if you check the root directory, there you should find a new folder named "**translations**", and if you look at the YAML configuration file, you will find a file named **translations.yaml**:

```
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

```
$lang = new Translate('en');
// or
$lang = Translate::use('en');

// Then, get the translation
$text = $lang->get('my.translation');
```

If the language is not specified, it will use the **default language**. However, you can also detect the user's language automatically:

```
$langCode = Translate::browserLanguage();
$t = new Translate($langCode);
```

However the user language could not be supported by your application, so you can also use this method:

```
$langCode = Translate::browserSupportedLanguage();
```

In this case, you will get the browser language **if supported**. If not, the default language will be used. A faster way to get the Translate object is:

```
$t = Translate::use('user');
$t->get('my.translation');
```

### Change the language

The user's language can be changed by running this:

```
Translate::setLanguage('fr');
```

**If cookies are enabled**, this will create a new cookie to remember the language chosen by the user. Then, this is the language obtained when running:

```
Translate::use('user');
```

This line will use the language chosen by the user (cookie), and if the cookie does not exist, then the browser supported language, and finally the default language.

**If cookies are not enabled**, the value will be stored in the session and lost soon.

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

### Parameters

Translations can carry dynamic parameters:

```
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

```
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
**Merge** only needs to be run once, from then on, the modification will be available everywhere through new Translate instances.
{% endhint %}
