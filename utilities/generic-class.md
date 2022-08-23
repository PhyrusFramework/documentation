# Generic class

The generic class is a way to convert an array to an object and vice versa:

```php
$array = [ 
    'name' => 'Example', 
    'url' => 'https://...' 
];

$obj = new Generic($arr);
// or
$obj = Generic::instance($arr);

$obj->name;
$obj->url;

// Back to array
$arr = $obj->toArray();

if (!$obj->has('name')) {
    $obj->set('name', $value);
} else {
    $obj->remove('name');
}

if ($obj->hasAndIs('name', 'Example')) // true!
if ($obj->hasAndIsNot('name', 'Example')) // false

if ($obj->isEmpty())
```

A Generic object can also be used to build dynamic structures with custom properties and methods **without creating a class**:

```php
function buildObject() {

    $g = new Generic();
    
    $g->set('numbers', []);
    
    $g->set('addNumber', function(...$numbers) use ($g) {
        foreach($numbers as $n) {
            $g->numbers[] = $n;
        }
    });
    
    $g->set('sum', function() use ($g) {
        $total = 0;
        foreach($g->numbers as $n) {
            $total += $n;
        }
        return $total;
    });
    
    return $g;
}

$obj = buildObject();
$obj->addNumber(3, 5, 8);
echo $obj->sum(); // 16
```
