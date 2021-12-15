---
description: Expands the power of the ORM to another level
---

# Advanced ORM

The basic ORM class seen before is a 1:1 relation of a model class to a database table. Example: class User -> table users.

But, most of the times when developing any platorm, the reality is that an entity is often composed by multiple tables, commonly one of these:

* **Metadata**: dynamic values
* **Translations**: translatable strings
* **Resources**: attached files, images

**Metadata** refers to dynamic data stored as a pair (key-value). Imagine that we have users, and we might have this information about them: address, phone, city, country, language, preferences, etc. We can't (**and must not**) create a column for each value, especially if most of them could be empty.

Instead we use a different table (users\_meta) with the columns (userId, key, value), and this can store infinite dynamic and different data about each user.

So, the **AdvancedORM** class **extends the previous ORM class** but also considers an entity composed by these 4 tables:

* xxx
* xxx\_metadata
* xxx\_translations
* xxx\_resources

{% hint style="info" %}
During **development mode**, tables are automatically created **when used**, so each ORM will only create the required tables, not all of them.
{% endhint %}

The declaration is exactly like a basic ORM:

```
class User extends AdvancedORM {
    function Definition() {...}
}
```

Then this class includes methods to control the additional features:

```
$user->setMeta('address', $address);
$address = $user->getMeta('address');
$user->setMeta('address', null); // remove

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

Resources refers to files, like images or PDFs. However, **uploading and storing** that file in the server is up to you and not related to the ORM.

The ORM will just store the **path** to the file. The method **addResource** will give us a **ORMResource** object.

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

However, there are **two different types** of resources:

* Single resource (ex: Profile photo)
* Multiple resources (ex: Album photos)

In the first case, when we upload a new version, the old must be replaces (new profile photo), in the second case we can have multiple album photos and add more to the list.

So a user **can have multiple resources per name**, unlike with metadata. That's why we use **addResource** instead of setResource.

So we need to detect if there was already a resource and replace it:

```
// Single
$res = $user->getResources('profile'); // list
if (sizeof($res) > 0) {
    $res = $res[0]; // First resource
    $res->setFile($newFile);
} else {
    $user->addResource('profile', $newFile);
}

// or
$res = $user->getResource('profile'); // first
if ($res != null) {
    $res->setFile($newFile);
}

// Multiple
$res = $user->addResource('profile', $file);
```

#### Sorting resources

When we have multiple resources, we may want to re-order them. For example, a user may want to change the order of his album photos.

So each Resource has a position property, and you will get them ordered by this position. By default the position will be the order of insertion (1, 2, 3, 4, 5...).

We can re-order the resources using their **move** methods:

```
$res = $user->getResources('photos')[3]; // Position 4

$res->moveUp();  // 4 <-> 3
$res->moveDown(); // 4 <-> 5
$res->moveToTop(); // 4 <-> 1
$res->moveToBottom(); // 4 <-> x
$res->moveTo($x); // 4 <-> x
```
