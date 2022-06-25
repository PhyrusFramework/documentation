---
description: Read or modify the configuration file from terminal
---

# CLI Config

The Config command is used to read or modify the project configuration files.

```
// Display all configuration
php cli config show

// Specific configuration
php cli config show database
php cli config show database.username

// Modify a configuration file
php cli config set database.username "myDBUser"
```
