---
description: Expands the power of the ORM to another level
---

# Advanced ORM

The basic ORM class seen [before ](orm.md)is a 1:1 representation of a database table.&#x20;

class User --> table users

But, usually when developing an application, the reality is that an entity is composed of mutiple tables such as these:

* ****[**Metadata**](metadata.md): dynamic values
* ****[**Translations**](translations.md): translatable strings
* ****[**Resources**](resources.md): attached files, images, documents

Hence, the **AdvancedORM** class **extends the previous ORM class,** but also uses these 4 tables:

* xxx
* xxx\_metadata
* xxx\_translations
* xxx\_resources

The declaration works exactly like the basic ORM:

```php
class User extends AdvancedORM {
    function Definition(DBBuilder $builder) {...}
}
```

### Create the tables

{% hint style="info" %}
During **development mode** tables are automatically created **when the ORM is used**, but in production mode you should create a migration or a script to create the tables.
{% endhint %}

To create the tables of a model, you can run this line:

```php
(new Model())->CheckTable(true);  // true to create also the additional tables
```

### Change the name of the tables

By default the extra tables will be named as the model table + '\_whatever':

```php
users, users_metadata, users_translations, users_resources
```

If you don't like these names, you can change any of them using these methods:

```php
class User extends AdvancedORM {
    function meta_table() {
        return 'user_meta';
    }
    function translations_table() {
        return 'user_locales';
    }
    function resources_table() {
        return 'user_files';
    }
}
```

### The reference column

These tables (meta, translations and resources) will reference the **ID** of the object in its table with a **Foreign Key**. By default, the foreign key column will be the same as the table name + "\_id":

products --> products\_id

If you don't agree with this nomenclature, you can customize the name of this column with the **reference\_column** method:

```php
class Product extends AdvancedORM {

    function reference_column() {
        return 'product_id';
    }

}
```
