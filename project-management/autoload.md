---
description: Autoload PHP files only when needed
---

# Autoload

One of the most amazing features of PHP is the capability of importing code files only when required using the **autoload** feature. When a class is used but does not exist, you can then import the file containing that class (or any additional files), and the line will be re-executed.

```
// Default PHP:
spl_autoload_register( function ($classname) {
    if ($classname == 'MyClass') {
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

**Autoload** is a function that receives **the name of the class** as first parameter, and **the files to import** as second. In both cases you can pass a single string, or an array containing multiple.

If multiple classes start with the same prefix, then you can use 'Prefix\*' instead of writing them manually.

{% hint style="info" %}
It is recommendable that you use autoload to import any PHP file that is not necessary globally, this way you make sure that these files are only imported when used, and your project's performance will be improved.
{% endhint %}
