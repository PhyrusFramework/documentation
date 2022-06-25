# Scripts

You can create php scripts and run them with the CLI. The difference with running a simple php file, is that scripts have previously loaded the framework and your project, so all those functions and classes will be available.

To create scripts, just create a folder named **/scripts** in the root directory and place php files there. To run a php file use the following command:

```
php cli script <name>
```

Use the name without the extension. For example: **/scripts/check-files.php**:

```
php cli script check-files
```

This is very useful to run tasks from the terminal.
