---
description: Read or modify the configuration file from terminal
---

# CLI Config

The Config command is used to read or modify the project configuration files from the terminal.

```
// Display all configuration
php phyrus config show

// Specific configuration
php phyrus config show database
php phyrus config show database.username

// Modify a configuration file
php phyrus config set database.username "myDBUser"
```
