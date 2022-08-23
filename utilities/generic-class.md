# Generic class

The generic class is a way to convert an array to an object and vice versa:

```
$array = [ 
    'name' => 'Example', 
    'url' => 'https://...' 
];

$obj = new Generic($arr);
// or
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

A Generic object can also be used to build dynamic structures with custom properties and methods **without creating a class**:

```
function buildObject() {

    $g = new Generic();
    
    $g->set('addPrintMethod', function() use ($g) {
        $g->set('print', function() {
            echo 'Hi!';
        });
    });
    
    return $g;
}

$obj = buildObject();
$obj->print();    // ERROR! Property 'print' does not exist

$obj->addPrintMethod();
$obj->print();    // Hi!
```

Another example:

```
function numberPack() {

    $g = new Generic();
    $g->set('numbers', []);
    
    $g->set('add', function(...$numbers) use ($g) {
        foreach($numbers as $n)
            $g->numbers[] = $n;
    });
    
    $g->set('total', function() use ($g) {
        $t = 0;
        foreach($g->numbers as $n) {
            $t += $n;
        }
        return $t;
    });
    
    return $g;
}

$pack = numberPack();
$pack->add(3, 6, 7, 2, 9);
$total = $pack->total();  // 27
```
