---
description: Configure the settings of your project
---

# Configuration

You'll find the configuration of your project inside the **/config** directory. There you will find some **YAML** files: database.yaml, web.yaml, project.yaml. Each one handles different configurations, it's just a matter of organization, you can even create your own custom yaml files.

While in development mode (project.yaml--> development\_mode = true) the YAML files will be combined into a **JSON** file that will appear in that folder when you run the website.

In production mode (project.yaml --> development\_mode = false) that JSON file will **only** be created if didn't exist, so **delete** it in order to force an update.

### Read/Write from Configuration

From code you can easily **read** from and **write** to the configuration files using the class **Config**:

```
$version = Config::get('project.version');
// project.yaml -> version

$db_user = Config::get('database.username');
// database.yaml -> username
```

The first word is the name of the **yaml** file, the following words are the path to the seeked value.

To change the configuration, you can do it only **at runtime during this execution without writing to the files** or **overwrite the files**:

```
Config::set('project.version', '2.0'); // Only for this thread
Config::save('project.version', '2.0'); // Write the file
```

If you save a value that didn't exist, it will be created:

```
Config::save('custom.my.custom.value', 23);
// custom.yaml --> [ my => [ custom => [ value => 23 ] ] ]

$value = Config::get('custom.my.custom.value');
```
