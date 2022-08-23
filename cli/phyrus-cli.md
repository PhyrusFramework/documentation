# Phyrus CLI

Phyrus includes a custom CLI with multiple commands to manage your project. Furthermore, this CLI is extendible. This means that you can create your own custom CLI commands.

The root folder of the project includes a file named "phyrus" without extension. That's the entry point to the CLI, and in the terminal you will run:

```
php phyrus <command> <parameters> --<flags>
```

### Create custom commands

To create a custom CLI command first you need to create a class extending the **CLI\_Module** class:

```php
class CLI_MyCommand extends CLI_Module { }
```

Then you need to register this module to the CLI:

```php
CLI::registerModule('<command>', '<class>');
CLI::registerModule('my-command', 'CLI_MyCommand');
```

You can do all of this in the same file, for example, under the **/back-end** directory.

From here on, you can develop two kind of commands:

* **Single action** commands
* **Sub-actions** commands

A single action command only uses one word (parameter):

```
> php phyrus my-command
```

In this case implement the **run**() method:

```php
class CLI_MyCommand extends CLI_Module {
    
    function run() {
        // Do something here
    }
    
}
```

A command with sub-actions uses a second command after the first one:

```
php phyrus my-command actionOne
php phyrus my-command actionTwo
php phyrus my-command actionThree
```

In this case, for each action create a method named **command\_\<name>**:

```php
class CLI_MyCommand extends CLI_Module {
    
    function command_actionOne() {
        // Do something here
    }
    
    function command_actionTwo() {
        // Something else here
    }
    
    // If run() is implemented, it overrides the
    // previous methods, so you have to check it yourself.
    function run() {
        if ($this->command == 'actionOne')
            // do something...
        else if ($this->command == 'actionTwo')
            // something else...
    }
}
```

In a **CLI\_Module** there are three **properties**:

* command (first parameter)
* parameters (following parameters)
* flags (parameters starting with --)

```php
php phyrus my-command opt-assets "./src/assets" --compress --type=css

// Result:
$this->command => 'opt-assets'
$this->parameters => [ './src/assets' ]
$this->flags = [
    compress => true,
    type => 'css'
]
```

### Help for commands

All commands have a **help** message that is displayed when used with the parameter help:

```
php phyrus help
php phyrus front help
php phyrus config help
```

To create a **help** message, implement a help method in your command and output the message:

```php
class CLI_MyCommand extends CLI_Module {

    function help() { ?>
        This is the help message.
    <?php }
    
}
```
