---
description: Translate your application
---

# Translations

Phyrus includes a system for managing translations through the class **Translate**. When you use the class for the first time it will **get installed** by adding new items to the configuration file (**config.json**) and creating the folder and **json files** for each language (by default only english). Just run:

```
new Translate();
```

Then, if you check your root folder, there you should see a new directory named "**translations**", and if you look at your configuration file, you will see this new object:

```
translate: {
     use_cookies: true,
     default_language: "en",
     supported_languages: ["en"],
     inherit: [],
     directory: "/translations",
     javascript: false
}
```

| Configuration        | Description                                                        |
| -------------------- | ------------------------------------------------------------------ |
| use\_cookies         | Use cookies to store the current language of the user              |
| default\_language    | Language to be used by default                                     |
| supported\_languages | **explained next**                                                 |
| inherit              | **explained next**                                                 |
| directory            | Folder containing translations                                     |
| javascript           | Define translations in Javascript so they can be used in front-end |

To translate first we need to create a **Translate** object using the desired language:

```
$lang = new Translate('en');
// or
$lang = Translate::use('en');

$text = $lang->get('my.translation');
```

If the language is not specified, it will use the **default language**. However, you can also detect the user's language automatically:

```
$langCode = Translate::browserLanguage();
```

The problem is that the user language could not be supported by your application, so you can also use this method:

```
$langCode = Translate::browserSupportedLanguage();
```

In this case, we will get the browser language **if supported**. If not, we will get the default language.

A better way to do this is:

```
$lang = Translate::use('user');
```

### Change the language

You can implement a language switcher in your website. Then, when changing the language, you need to run this line:

```
Translate::setLanguage('fr');
```

**If cookies are enabled**, this will create a new cookie to remember the language chosen by the user. Then, this is the language you will get when running:

```
Translate::use('user');
```

This line will use the language chosen by the user (cookie), and in the cookie does not exist, then the browser language.

**If cookies are not enabled**, the value will be stored in the session and lost soon.

### Inheritance

In some countries, multiples languages are spoken. So a speaker from one of those languages will probably speak the others.&#x20;

For example, in Ukraine both Ukrainian and Russian are spoken, so if you support russian but not ukrainian, and your default language is english, your ukrainian users should see the website in russian, not english.

Another example, catalan is another language spoken in Spain, so catalan speakers should see the website in spanish, not english.

To solve this problem, there is a configuration name **inherit**. Here you need to "**redirect**" unsupported languages to supported languages:

```
default_language: 'en',
supported_languages: ['en', 'es', 'ru'],
inherit: {
   uk: "ru",
   ca: "es"
}
```

With this configuration, when using **Translate::browserSupportedLanguage()** or **Translate::instance('user')** an ukrainian user would get russian, not english:

* First check if the language browser is supported
* If not, **check inheritance**
* If not, then default language

### Dynamic translations

Translations are stored as JSON files in your translations directory. However, you might want to load translations dynamically on runtime.

To do it, you need to **merge** an array to your translations object:

```
Translate::use('en')->merge([
    'pages' => [
        'checkout' => [
            'purchase' => 'Purchase'
        ]
    ]
]);
```

Obviously, if the translation already existed, it will be overwritten.

{% hint style="info" %}
You only need to run **merge** once, from then on, the modification will be available everywhere through new Translate instances.
{% endhint %}
