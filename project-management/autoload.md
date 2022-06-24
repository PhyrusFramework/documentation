---
description: Autoload PHP files only when needed
---

# Autoload

One of the most amazing features of PHP is the capability of importing a file only when the class inside is used, and not when it's not needed using the **autoload** feature. This improves the project performance greatly, because you may have a huge project full of code, but every process only loads the required files and ignores the rest.

To do it, you can define a **callback** that is called whenever an unknown class is used:

```
// Default PHP:
spl_autoload_register( function ($classname) {
    if ($classname == 'MyClass') {
        // Import the file with that class
        require_once( $pathToFile );
    }
});
```

Phyrus simplifies and improves this functionality with a method called simply **autoload**:

```
// Single:
autoload( 'MyClass', __DIR__ . '/MyClass.php' );

// Multiple:
autoload( ['ClassA', 'ClassB', 'classC' ], [$file1, $file2] );
// or also:
autoload( 'Class*', [$file1, $file2]);
```

**Autoload** is a function that receives **the name of the class** as first parameter, and **the files to import** as second. It can also detect mutiple classes, and import multiple files as consequence.

If multiple classes start with the same prefix, then you can use 'Prefix\*' instead of writing them manually.

{% hint style="info" %}
It is recommendable that you use autoload to import any PHP class that is not necessary globally, this way you make sure that these files are only imported when used, and your project's performance will be improved.
{% endhint %}
