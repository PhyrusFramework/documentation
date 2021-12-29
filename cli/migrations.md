# Migrations

Migrations are used to create revertible modifications to the project, usually to the database. For example, modifying existing tables or filling them with data.

To create migrations, create a folder named **migrations** in the root. Then create php files there and, inside, create instances of the class **Migration** which receives two functions in the constructor: **do** and **undo**:

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
Therefore, it is recommendable to name your migrations with a numeric prefix, such as 0001\_xxx.php, 0002\_xxx.php, ...
{% endhint %}

Once executed, a **json** file will be created in the folder (**history.json**) registering which migrations where executed on what date. Then, if you run the command again, those migrations **won't be executed again**.

If you want to undo migrations, then execute:

```
php cli migrate undo
```

This will undo the migrations in the inverse order in which they were applied:

A, B, C <--> C, B, A

So all changes will be undone.

### Specific migrations

You can also migrate or undo a specific migration. To do it, add its name (without the .php extension) to the command:

```
php cli migrate 0003
php cli migrate undo 0003
```

However, if you try to run or undo a migration that had already been executed, you will receive a warning message:

{% hint style="danger" %}
The migration '\<name>' wants to be executed but it was already migrated. Run with --force to execute anyway
{% endhint %}

Then, run the command with --force to migrate anyway:

```
php cli migrate 0003 --force
```

### Start over

If you want to delete the history and execute all migrations again, use the flag --fresh:

```
php cli migrate --fresh
```
