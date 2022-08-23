# Utility functions

Phyrus adds some utility functions to help the developer with common tasks:

### Generate a password

```php
$hash = generate_password( 'watermelon' );
```

This password then can be verified using the native PHP function **password\_verify**:

```php
password_verify( 'watermelon', $hash );
```

### Unique identifier (GUID)

Generate a unique identifier:

```php
$id = GUID();
```

### Date now

Obtain **now** as a datetime string:

```php
$now = datenow();  // YYYY-MM-DD HH:mm:ss
```

### Detect OS

Detect **the server's** Operative System, possible values are 'windows', 'osx' or 'linux':

```php
if (detectOS() == 'windows')
    // windows command
else
    // linux command
```

### Escape HTML

Escape HTML characters to avoid XSS attacks:

```php
$escaped = e($html);
```

### Get the user IP

```php
$ip = IP();
```

### Caller

This method tells you which file called the current function (where this method is executed). Very useful to debug when you have an error and you don't know where it came from.

```php
'Error comes from ' . caller();
```

### Forn

It's just a for. Repeats an action n times.

```php
forn(100, function() {
    // do something
});
```

### CMD

Executes a command line and **echoes** the output.

```php
cmd('df -H');
```

### GeoDistance

This function calculates the distance between two coordinates (in meters):

```php
$meters = geoDistance($lat1, $lng1, $lat2, $lng2);
```
