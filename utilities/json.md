# JSON

The JSON class helps you manage JSON objects and strings.&#x20;

It is an improvement to the **json\_encode/decode** php function. For example, it handles the latin characters encoding automatically, so the json string does not break when using special characters.

It can be used in both directions: String to JSON and JSON to String, or even convert it to an array or object:

```
$json = new JSON();  // empty
$json = new JSON($string);  // Parse string
$json = new JSON($arr);    // from array
$json = JSON::instance($str/arr);

// Modify
$json->$key;
$json->set($key, $value);
$json->remove($key);

$arr = $json->toArray();
$obj = $json->toObject(); // Generic object
$str = $json->string($pretty? = false);

// Direct array <-> string
$arr = JSON::parse($str);
$str = JSON::stringify($arr);

// Check if string is a JSON:
if (JSON::isJSON($str))
```

You can also directly read/write from a file:

```
$json = JSON::fromFile($path);
$json->set($key, $value);
$json->saveTo($path);
```

