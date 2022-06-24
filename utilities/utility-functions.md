# Utility functions

Phyrus adds some PHP functions for mulltiple purposes:

### Generate a password

```
$hash = generate_password( 'watermelon' );
```

This password then can be verified using the native PHP function **password\_verify**:

```
password_verify( 'watermelon', $hash );
```

### Unique identifier (GUID)

Generate a unique identifier:

```
$id = GUID();
```

### Date now

Obtain **now** as a datetime string:

```
$now = datenow();  // YYYY-MM-DD HH:mm:ss
```

### Detect OS

Detect **the server's** Operative System, possible values are 'windows', 'osx' or 'linux':

```
if (detectOS() == 'windows')
    // windows command
else
    // linux command
```

### Escape HTML

Escape HTML characters to avoid XSS attacks:

```
$escaped = e($html);
```
