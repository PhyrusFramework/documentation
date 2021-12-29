# Generic class

The generic class is a way to convert an array to an object and vice versa:

```
$arr = [ 'name' => 'Example', 'url' => 'https://...' ];
$obj = new Generic($arr);
$obj = Generic::instance($arr);
$arr = $obj->toArray();

$obj->name;
$obj->url;

if (!$obj->has('name')) {
    $obj->set('name', $value);
} else {
    $obj->remove('name');
}

if ($obj->hasAndIs('name', 'Example')) // true!
if ($obj->hasAndIsNot('name', 'Example')) // false

if ($obj->isEmpty())
```
