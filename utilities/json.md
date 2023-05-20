# JSON

The JSON class is an improvement to the **json\_encode/decode** native php function. For example, it handles latin characters encoding automatically, so the json string does not break when using special characters.

It can be used in both directions: String to JSON or JSON to String, or even convert it to an array or object directly.

Most of the time it will be used to parse directly from string to array and viceversa:

```php
$arr = JSON::parse($json);
$json = JSON::stringify($arr);
```

But the JSON object can also be used to build JSON strings dynamically operating on the JSON object:

```php
$json = new JSON();  // empty
$json = new JSON($string);  // Parse string
$json = new JSON($arr);    // from array
$json = JSON::instance($str/arr);

$json = new JSON('{"name": "Phyrus"}');

echo $json->name;
$json->set('description', $value);
$json->remove('name');

$arr = $json->toArray();
$arr['name'];

$obj = $json->toObject(); // Generic object
$obj->name;

// Convert to JSON string
$str = $json->string($pretty? = false);

// Check if string is a JSON:
if (JSON::isJSON($str))
```

You can also directly read/write from a file:

```php
$json = JSON::fromFile($path);
$json->set('newField', $value);
$json->saveTo($path);
```

