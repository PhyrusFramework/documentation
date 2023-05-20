# Migrations

Migrations are used to create revertible modifications to the project, usually to the database, but could be any kind of modification. They are very similar to Scripts, but with the difference that:

* Migrations can be done and undone.
* Migrations are stored in the database to remember which one was already executed and when.

To create a migration use the command:

```
php phyrus migrate create <name>
```

The file will be created inside a new directory named **/migrations** in the root directory. This file will contain the creation of a **Migration** object which received two functions in its constructor, **do** and **undo**:

```php
// /migrations/0001_create_logs_table.php
<?php
new Migration(

    function() {
        // Do
        DB::createTable('logs', [
            // ... columns
        ]);
    },
    
    function() {
        // Undo
        DB::table('logs')->drop();
    }
);
```

Inside these functions you need to manually write the code to **undo** what you've done in the first function.

Then, you can run **all pending** migrations with the command:

```
php phyrus migrate
```

This will run your pending migrations (the ones that were not migrated yet) in **alphabetical order**.

{% hint style="info" %}
When a migration is created with the CLI command, the date is added as a prefix to the name of your migration, to make sure that migrations are executed in the right order.
{% endhint %}

If a database is connected, a new table named "**migrations**" will be created to store which migrations where already executed and when. If there's not a database connected, which means that you purposely want a project without a database, then a **JSON** file will be created in the migrations directory to store that same information.

If you want to **undo** migrations, then execute:

```
php phyrus migrate undo
```

This will undo the migrations in the reverse order in which they were applied:

A, B, C <--> C, B, A

So all changes will be undone.

### Run specific migrations

You can also migrate or undo a specific migration. To do it, add its name (without the .php extension) to the command:

```
php phyrus migrate <name>
php phyrus migrate undo <name>
```

However, if you try to do or undo a migration that had already been executed, you will receive a warning message:

{% hint style="danger" %}
The migration '\<name>' wants to be executed but it was already migrated. Run with --force to execute anyway.
{% endhint %}

Then, if you insist in executing a migration that had been already migrated, run the command with --force to migrate anyway:

```
php phyrus migrate <name> --force
```

### Start over

If you want to delete the history and execute all migrations again, use the flag --fresh:

```
php cli migrate --fresh
```

{% hint style="danger" %}
This will delete your history **without undoing** the migrations and then run the migrations again. If what you want is to undo all migrations, just run undo.
{% endhint %}
