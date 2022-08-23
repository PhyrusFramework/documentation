---
description: Manage and modify strings
---

# Text

The class **Text** is used to operate on strings:

```php
$text = new Text( 'hello ');
$text = Text::instance('hello');
```

### Split

Equivalent to explode. But multiples delimiters can be used, and a second parameter can be used to avoid empty strings.

```php
split( string/array, $empty? = true)

$list = Text::instance( 'A, B, C' )->split(',');    
// [A, B, C]

$list = Text::instance( 'A-B/C//D-E' )->split( [ '/', '-' ], false );   
// [A, B, C, D, E]
```

### Between

Get the string between the first occurrance of characters.

```php
$good = Text::instance( 'Hey, (good) morning!' )->between( '(', ')' );
```

### Lower and upper case

```php
$lower = Text::instance( 'Hello, How Are You?' )->toLower();
$upper = Text::instance( 'Hello, How Are You?' )->toUpper();
```

### Sanitize

Sanitize converts a string into a usable identifier:

```php
$id = Text::instance('This is the title')->sanitize();
// this-is-the-title
```

You can specify custom character conversion with a parameter:

```php
$id = Text::instance('This is the title')->sanitize([
    ' ' => '_'
]);  
// this_is_the_title
```

### **If text starts/ends with**

Check if text starts or ends with string.

```php
if ( Text::instance( 'hello world' )->startsWith( 'hello' ) )
if ( Text::instance( 'hello world' )->endsWith( 'world' ) )
```

### Contains

```php
if ( Text::instance( 'My name is profesor Oak' )->contains( 'name' ) )
```

### **Reverse**

```php
$reverse = Text::instance('hello')->reverse();   // olleh
```

### **IndexOf**

```php
$position = Text::instance( 'This is a text' )->indexOf( 'is a' );
```

### **Replace**

```php
$label = Text::instance( 'User: <username>' )->replace( '<username>', 'Admin' );
```

### **Random**

Generates a random string. Default length: 20.

```php
$code = Text::random();
$code = Text::random( 5 );
```

### **Similarity**

Calculates the similarity % between two texts:

```php
$percentage = Text::similarity( 'This is a text', 'This is some text' );
```

### isNumber

```php
if (Text::instance('12345')->isNumber() )
```

### Match

Uses regex to check if the string matches a pattern. However, it automatically transforms the \* to regex:

```php
Text::instance('UserPost')->match('User*');  // true
Text::instance('TheUserPost')->match('*User*'); // true
Text::instance('TheUser')->match('*User'); // true
```
