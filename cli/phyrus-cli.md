# Phyrus CLI

Phyrus includes an extendible CLI. This means that you can create your own custom CLI commands to execute.

The root folder of the project includes a file named "cli" without extension. That's the entry point to the CLI, and in the terminal you will run:

```
php cli <command> <parameters> --<flags>
```

In the next articles you will learn each CLI command provided by the framework.

### Create custom commands

To create a custom CLI command first you need to create a class extending the **CLI\_Module** class:

```
class CLI_MyCommand extends CLI_Module { }
```

Then you need to use:

```
CLI::registerModule('<command>', '<class>');
CLI::registerModule('my-command', 'CLI_MyCommand');
```

You can do all of this in the same file, for example, under the **/src/code** directory.

From here on, you can develop two kind of commands:

* **Single action** commands
* **Sub-actions** commands

A single action command only uses one word (parameter):

```
> php cli my-command
```

In this case use the **run**() method:

```
class CLI_MyCommand extends CLI_Module {
    function run() {
        // Do something here
    }
}
```

A command with sub-actions uses a second command:

```
php cli my-command actionOne
php cli my-command actionTwo
php cli my-command actionThree
```

In this case, for each action create a method command\_\<name>:

```
class CLI_MyCommand extends CLI_Module {
    
    function command_actionOne() {
        // Do something here
    }
    
    function command_actionTwo() {
        // Something else here
    }
    
    // If run() is implemented, it overrides the
    // previous methods:
    function run() {
        if ($this->command == 'actionOne')
            // do something...
        else if ($this->command == 'actionTwo')
            // something else...
    }
}
```

Inside a CLI\_Module there are three properties:

* command (first parameters)
* parameters (next parameters)
* flags (optional values with --)

```
php cli my-command opt-assets "./src/assets" --compress --type=css

$this->command => 'opt-assets'
$this->parameters => [ './src/assets' ]
$this->flags = {
    compress: true,
    type: 'css'
}
```
