# Resources

Resources refer to files, like images or PDFs. However, **uploading and storing** the file in the server is up to you and not managed by the ORM.

The ORM will just store the **path** to the file. The method **addResource** will return an **ORMResource** object.

```
$resource = $user->addResource($type, $file);
$resource = $user->addResource('profile_photo', '/uploads/images/xxx.jpg');

$resource->ID;
$resource->file;

// Edit
$resource->setFile($file);
$resource->delete();

$res = $user->getResourceById($ID);
$res = $user->getResourceByFile($file);
```

However, there are **two different cases**:

* Single resource (ex: Profile photo)
* Multiple resources (ex: Album photos)

In the first case, when the user uploads a new file, the previous must be replaced (new profile photo), in the second case the user can have **multiple** album photos and add more to the list.

So a user **can have multiple resources of a type**. That's why the method is called **addResource** instead of "setResource".

So, in the first case we need to detect if there was already a resource and **replace** it:

```
// Single file
$profilePhotos = $user->getResources('profile');

if (sizeof($profilePhotos) > 0) {
    $res = $profilePhotos[0]; // First resource
    $res->setFile($newFile);  // Update
} else {
    // Create new
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

So each Resource has a **position** property, and they will be obtained sorted by this position. By default the position will be the order of insertion (1, 2, 3, 4, 5...).

But they can be re-ordered by using the **move** methods:

```
$res = $user->getResources('photos')[3]; // 4th photo

$res->moveUp();  // 4 -> 3
$res->moveDown(); // 4 -> 5
$res->moveToTop(); // 4 -> 1
$res->moveToBottom(); // 4 -> n
$res->moveTo($x); // 4 -> x
```

