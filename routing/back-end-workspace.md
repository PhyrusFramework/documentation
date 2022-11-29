# Back-End workspace

The **/back-end** directory is a free **workspace** for you to work as you like. The framework **does not force you any file-directory structure** in here, so you can decide how you organize your project.

Inside the directory, you will find a file named **autoload.php** with this content:

{% hint style="info" %}
This uses the PHP **autoload** feature. If you don't know this, PHP has a feature that allows you to import files only when needed and not always, to improve the performance of the project. When a **class** is used but it does not exist, PHP will consult these specifications and then import the indicated files. Then it will retry the line that failed.

[https://www.php.net/manual/en/language.oop5.autoload.php](https://www.php.net/manual/en/language.oop5.autoload.php)
{% endhint %}

```php
<?php

return [
    'always' => [
        '/endpoints'
    ],

    'classByFile' => [
        '/models'
    ],

    'classByName' => [
        'MyClass' => [$file1, $file2, $file3...]
    ]
];
```

This file defines three sections:

* **Always**: list of files or directories that are **always** loaded in every request. This means that everytime that a user uses your API those files will be imported.
* **ClassByFile**: Here you list files or directories when the PHP file is named exactly like the class inside (ex: User.php -> class User).
* **ClassByName**: Here you indicate the name of a class and, if it's not recognized when used, then will import the following files.

{% hint style="info" %}
When the path to a directory is used instead of a file, that loads all the php files inside and **in sub-directories recursively**.
{% endhint %}

The **always** section **must** be used at least for **routing files** using the **Manual** or **CRUD** methods. Obviously, because the Router must always be aware of the routes in the project, in order for the API to work.

However, in many other cases the second section **ClassByFile** will be the most useful. It allows you to load files only when they are needed and not always, which improves performance significantly. For example, this is a very good place to import your **models** (also called **entities**), so each endpoint of your API will only load the classes that needs to work, not all of them.

In the example above, it will use the directory **/back-end/models**. That means that, for all PHP files placed in this directory **or sub-directories**, now PHP knows that every of those files contains the class named like the file. If there's a file named "**Product.php**", your project now knows that whenever the class "**Product**" is needed, it must load that file. If it's never used, it will never be imported.

And finally the last section, **ClassByName**, allows you to tell php: "hey, if my code asks you to use **this** class, then import all these files". This feature can be very useful if you have a feature that is actually composed of multiple PHP files and classes (like a local library) that you don't want to import unless it is necessary. So, whenever the code tries to use that class, it will trigger the import of multiple php files.

Now, with these three auto-importing methods, feel free to organize your **/back-end** directory as you like. Instead of forcing you a structure, Phyrus gives you freedom to setup and customize your worshop.
