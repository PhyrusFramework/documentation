# Migrations

Migrations are used to create revertible modifications to the project, usually to the database. For example, modifying existing tables or filling them with data.

To create a migration use the command:

```
php cli migrate create <name>
```

The file will be created inside a new directory named **/migrations** in the root directory. This will contain your file with the definition of a class extending the **Migration** class which receives two functions in the constructor: **do** and **undo**:

```
// /migrations/0001_create_logs_table.php
<?php
new Migration(

    function() {
        // Do
        DBTable::create([
            'name' => 'logs',
            'columns' => [...]
        ]);
    },
    
    function() {
        // Undo
        DBTable::instance('logs')->drop();
    }
);
```

Then, you can run all migrations with the command:

```
php cli migrate
```

This will run your migration files in **alphabetical order**.

{% hint style="info" %}
When a migration is created with the CLI command, the date is added as a prefix to the name of your migration, to make sure that migrations are executed in the right order.
{% endhint %}

If a database is connected, a new table named "**migrations**" will be created to store which migrations where already executed and when. If there are not valid database credentials in the project, which means that you purposely want a Phyrus project without a database, then a **JSON** file will be created in the migrations directory to store that same information.

If you want to **undo** migrations, then execute:

```
php cli migrate undo
```

This will undo the migrations in the reverse order in which they were applied:

A, B, C <--> C, B, A

So all changes will be undone.

### Specific migrations

You can also migrate or undo a specific migration. To do it, add its name (without the .php extension) to the command:

```
php cli migrate xxxx
php cli migrate undo xxxx
```

However, if you try to run or undo a migration that had already been executed, you will receive a warning message:

{% hint style="danger" %}
The migration '\<name>' wants to be executed but it was already migrated. Run with --force to execute anyway
{% endhint %}

Then, run the command with --force to migrate anyway:

```
php cli migrate xxx --force
```

### Start over

If you want to delete the history and execute all migrations again, use the flag --fresh:

```
php cli migrate --fresh
```
