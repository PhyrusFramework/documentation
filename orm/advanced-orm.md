---
description: Expands the power of the ORM to another level
---

# Advanced ORM

The basic ORM class seen [before ](orm.md)is a 1:1 representation of a database table. Example: class User --> table users.

But, usually when developing an application, the reality is that an entity is composed of mutiple tables such as these:

* **Metadata**: dynamic values
* **Translations**: translatable strings
* **Resources**: attached files, images, documents

The **AdvancedORM** class **extends the previous ORM class,** but also considers an entity composed of these 4 tables:

* xxx
* xxx\_metadata
* xxx\_translations
* xxx\_resources

{% hint style="info" %}
During **development mode** tables are automatically created **when used**, but each ORM will only create the required tables when used, not all of them at once.
{% endhint %}

The declaration works exactly like the basic ORM:

```
class User extends AdvancedORM {
    function Definition(DBBuilder $builder) {...}
}
```

### Metadata

**Metadata** refers to dynamic data stored as a pair (key-value). Imagine that our application has users and these might have optional information about them such as: address, phone, city, country, language, preferences, etc. We can't (**and should not**) create a column for each of these values in the users table, especially if most of them could be empty because they are optional.

Instead, use a different table (**users\_meta**) with the columns (userId, key, value), and this can store infinite dynamic data about each user:

| user\_id | meta\_key | meta\_value         |
| -------- | --------- | ------------------- |
| 236      | address   | street nº9          |
| 236      | birth     | 1982-06-23 00:00:00 |
| 322      | address   | boulevard           |

```
$user->setMeta('address', $address);
$address = $user->getMeta('address');
$user->setMeta('address', null); // remove
```

This will allow you to easily add new data in the database without the need of modifying the structure of the database by adding or removing columns from tables.

### The reference column

These tables (meta, translations and resources) will reference the ID of the object in its table by a Foreign Key. By default, the foreign key column will be the same as the table + "\_id":

products --> products\_id

If we don't agree with this nomenclature, we can customize the name of this column with the **reference\_column** name:

```
class Product extends AdvancedORM {

    function reference_column() {
        return 'product_id';
    }

}
```

### Translations

```
$post->setTranslation('title', 'en', 'This is the title');
$post->setTranslation('title', 'es', 'Este es el título');
$title = $post->getTranslation('title', 'en');
```

Sometimes translations could be missing in some languages but exist in others. In that case, you can use **getAnyTranslation**:

```
$title = $post->getAnyTranslation('title', ['es', 'en', '*']);

1. Get translation in spanish (es)
2. If not exists -> in english (en)
3- If not exists -> in any available (*)
```

### Resources

Resources refer to files, like images or PDFs. However, **uploading and storing** the file in the server is up to you and not managed by the ORM.

The ORM will just store the **path** to the file. The method **addResource** will return an **ORMResource** object.

```
$resource = $user->addResource($name, $file);

// Edit
$resource->setFile($file);
$resource->ID;
$resource->file;
$resource->delete();

$res = $user->getResourceById($ID);
$res = $user->getResourceByFile($file);
```

However, there are **two different cases**:

* Single resource (ex: Profile photo)
* Multiple resources (ex: Album photos)

In the first case, when the user uploads a new file, the previous must be replaced (new profile photo), in the second case the user can have multiple album photos and add more to the list.

So a user **can have multiple resources of a type**. That's why the method is called **addResource** instead of setResource.

So, in the first case we need to detect if there was already a resource and replace it:

```
// Single
$profilePhotos = $user->getResources('profile');

if (sizeof($profilePhotos) > 0) {
    $res = $profilePhotos[0]; // First resource
    $res->setFile($newFile);
} else {
    $user->addResource('profile', $newFile);
}

// or also
$res = $user->getResource('profile'); // get first result
if ($res != null) {
    $res->setFile($newFile);
} else {
    $user->addResource('profile', $newFile);
}

// Multiple photos
$res = $user->addResource('album', $file);
```

#### Sorting resources

When there are multiple resources, we may want to re-order them. For example, a user may want to change the order of his album photos.

So each Resource has a position property, and they will be obtained sorted by this position. By default the position will be the order of insertion (1, 2, 3, 4, 5...).

But they can be re-ordered by using the **move** methods:

```
$res = $user->getResources('photos')[3]; // Position 4

$res->moveUp();  // 4 -> 3
$res->moveDown(); // 4 -> 5
$res->moveToTop(); // 4 -> 1
$res->moveToBottom(); // 4 -> n
$res->moveTo($x); // 4 -> x
```
