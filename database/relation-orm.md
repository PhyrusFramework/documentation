---
description: ORM to build relation tables
---

# Relation ORM

The class **RelationORM** works exactly like the basic ORM, except that it lets you use other ORMs as columns and those will be the primary key.

In the definition, those columns referencing other ORMs will use **the PHP class as key**:

```
class ProductCategory extends RelationORM {

    function Definition() {
        return [
            'name' => 'product_category',
            'columns' => [
                'Product' => [
                    'name' => 'product_id'
                ],
                'Category' => [
                    'name' => 'category_id'
                ],
                [
                    'name' => 'position',
                    'type' => 'INT'
                ]
            ]
        ]
    }

}
```

The first two columns reference the classes **Product** and **Category**.

{% hint style="info" %}
In these columns you don't need to specify the type or the foreign key, both are made automatically.
{% endhint %}

By default, **all foreign keys** will be the **primary** key together. However, you can manually specify which ones are the primary key:

```
'columns' => [
    'Product' => [
        'name' => 'product_id',
        'primary' => true
    ],
    'Category' => [
        'name' => 'category_id'
    ]
]
```

Now only the **product\_id** would be the primary key.

### Relation methods

A relation works like any other ORM, so you can use the same methods explained in the previous sections:

```
$rel->save();
$rel->delete();
$rel->getTable();
ProductCategory::Table();
ProductCategory::dropTable();
ProductCategory::find($where);
ProductCategory::findOne($where);
```

### Create relations

Relations are created just like normal ORM objects:

```
$rel = new ProductCategory();
$rel->product_id = $product->ID;
$rel->category_id = $category->ID;
$rel->save();
```

Then, when we want to retrieve the ORM object from the relation, we can use the method **getModel**:

```
$rel = ProductCategory::findOne('product_id = 26 AND category_id = 37');

// Option 1
$product = new Product($rel->product_id);
// Option 2
$product = $rel->getModel('product_id');
```

### Search models

You can easily find relations using the methods **find** and **findOne**. But additionally, you can find models directly using the method **modelByRelation**:

```
$products = ProductCategory::modelByRelation('product_id', 
    'category = :catID', [
        'catID' => 34
    ]);
    
$products is a list of Product objects.
```
