---
description: Configure the settings of your project
---

# Configuration

You'll find the configuration of your project inside the **/config** directory. There you will find multiple **YAML** files: database.yaml, web.yaml, project.yaml. Each one of these handles different configurations. It's just a matter of organization, **you can create your own custom yaml files**.

While in development mode (project.yaml--> development\_mode = true) the YAML files are combined and cached into a JSON file **every time you access**, while in production mode **it will only do it once.** So, if you change a configuration in production, then run:

```
php phyrus config clear
```

If for some reason you couldn't do it, then manually delete the file /vendor/phyrus/framework/config.json.

### Read/Write from Configuration

From the code you can easily **read and** **write** from/to the configuration files using the class **Config**:

```
$version = Config::get('project.version');
// project.yaml -> version

$db_user = Config::get('database.username');
// database.yaml -> username

Config::get('project.uploads.images.dir');
// project.yaml -> uploads.images.dir
```

The first word is the name of the **yaml** file, the following words are the path to the value.

To programmatically change a configuration, you can do it either **at runtime without overwriting the files** or **overwrite the files**:

```
Config::set('project.version', '2.0'); // Only for this process
Config::save('project.version', '2.0'); // Write the file
```

If you save a value that didn't exist, it will be created. If a YAML file needs to be created, it will:

```
Config::save('custom.my.custom.value', 23);
// custom.yaml --> [ my => [ custom => [ value => 23 ] ] ]

$value = Config::get('custom.my.custom.value');
```

### Environments

Inside the **project.yaml** file, there's an **environment** value. Phyrus will search inside the **/config** directory another **folder named like the environment**, and if exists will read its YAML files and **combine them with the previous configuration**.

For example, to use different database credentials with three different environments: **local**, **dev** and **prod**. Default configuration can be considered the **local** environment. Then, we would create two directories: **/config/dev** and **/config/prod**.

In them, add a file named **database.yaml** (like the one in the main configuration directory) and copy the same structure from the parent file, but add here only the values that change with respect to the default ones.

That's it. Now just change the project.yaml -> environment value to use a different configuration. If you need to automatize the process of changing the environment, remember you can modify configuration files programmatically by CLI:

```
> php phyrus config set project.environment prod
```

