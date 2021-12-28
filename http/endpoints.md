---
description: Create an API using Controllers
---

# Endpoints

An API is actually just a website, like any other, except that routes do not return HTML but another data format like JSON or XML.

So, in order to build an API endpoints, you need to use **Controllers** like with any other page. The difference is that the controller enabled the option **raw** to avoid HTML:

```
class ProductsController extends Controller {

    function init() {
        $this->raw = true;
    }

}
```

Then the **display** method is responsible for the endpoint logic:

```
class ProductsController extends Controller {
    function init() {
        $this->raw = true;
    }

    function display() {
        $req = new RequestData();
        // Accept only GET and POST
        $req->requireMethod('GET', 'POST');
        
        if ($req->method() == 'GET') {
            return $this->getProducts();
        } else {
            return $this->createProduct();
        }
    }
    
    function getProducts() {
        $offset = $req->has('offset') ?
            intval($req->offset) : 0;
    
        $products = Product::find("1 LIMIT 10 OFFSET $offset");
        
        // Convert ORM objects to Arrays
        $output = arr($products)->map(function($item) {
            return $item->toArray();
        })->toArray();
        
        return $output;
    }
    
    function createProduct() {
        $req->require('name', 'price');
        
        $product = new Product();
        $product->name = $req->name;
        $product->price = floatval($req->price);
        $product->save();
        
        return $product->toArray();
    }
}
```

You could output **JSON** with **echo** and the JSON class:

```
echo JSON::stringify($output);
```

However, this is not necessary because the Controller will do it **automatically** if you return an array:

```
function display() {
    return [
        'a' => 34
    ];
}

// Page displays  {"a":34}
```
