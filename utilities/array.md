# Array

The **Arr** class is a wrapper for arrays that lets you do multiple operations on it. To initialize one we can use the constructor or the **arr()** method:

```
$arr = new Arr([...]);
$arr = Arr::instance([...]);
$arr = arr([...]);
```

**Arr** objects behave partially like a normal array:

```
$arr = new Arr([...]);
$v = $arr['key'];
$arr['key'] = $v;
$arr[] = $newItem;

foreach($arr as $k => $v) {...}
```

The arr object can be converted back to an array using **getArray**():

```
$arr->getArray();
```

With the arr object we can make many operations to the array:

```
// map/iterate (like JS)
$list = $arr->map(function($item) {
    return $item->toArray();
});

if ($arr->has('key'))

$arr->size();
if ($arr->isEmpty())
$arr->first();
$arr->last();
$arr->last(1); // last -1
$arr->keys();

// Get random item
$arr->random();

// Is associative array?
$arr->isAssoc();

if ($arr->contains($value))

$arr->delete($key);

$arr->reverse();
$other = $arr->copy()->reverse();

$arr->print(); // Print as HTML
$arr->print(false); // Print as text
```

### Compare arrays

We can compare two arrays recursively using **equalTo**():

```
if ($arr->equalTo($another))
```

Accepts both an **array** or another **arr** object.

### Merge arrays recursively

```
$arr->merge($another, $mergeNoAssoc? = false);
```

The second parameter decides whether **no associative arrays** must be merged or not. An associative array is a dictionary, formed by pairs of key-value. When the array is not associative, it's a normal lineal list: \[a,b,c,d] where keys are the index position (0, 1, 2, 3).

When merging associative arrays, these may contain non-associative arrays, what's the right strategy then? Example:

```
Merge
[ 'lang' => 'en', 'languages' => ['en', 'es'] ]
&
[ 'language' => ['en', 'fr'] ]

// Option 1: Overwrite
Result:
[ 'lang' => 'en', 'languages' => ['en', 'fr'] ]

// Option 2: Mix
[ 'lang' => 'en', 'languages' => ['en', 'es', 'fr'] ]
```

Depending on the situation, non-associative arrays must be mixed or overwritten.

### Force structure

The **force** method converts an array to a desired structure with default values:

```
$arr->force($defaults);

$arr = arr(['lang' => 'js', 'framework' => 'vue']);
$arr->force([
    'lang' => 'php',
    'version' => '7.4'
]);

// Result
[
    'lang' => 'js',
    'version' => '7.4'
]
```

The "**framework**" key disappears because it was not specified in the **$defaults** structure. "**lang**" keeps its value because it was present in the array, while "**version**" was not and takes the default value.
