# Metadata

**Metadata** refers to dynamic information stored as a pair (key-value). Imagine that our application has users and these might have optional information about them such as: address, phone, city, country, language, preferences, etc. We **should not** create a column for each of these values in the users table, especially if most of them could be empty because they are optional.

Instead, use a different table (**users\_meta**) with the columns (user\_id, key, value), and this can store infinite dynamic data about each user:

| user\_id | meta\_key | meta\_value         |
| -------- | --------- | ------------------- |
| 236      | address   | St. Charles Street  |
| 236      | birth     | 1982-06-23 00:00:00 |
| 322      | address   | Washington Avenue   |

```php
$user->setMeta('address', $address);
$address = $user->getMeta('address');
$user->setMeta('address', null); // remove
```

This will allow you to easily add new data in the database **without the need of modifying the structure** of the database by adding or removing columns from tables.

