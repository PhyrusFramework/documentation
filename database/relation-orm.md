---
description: ORM to build relations between other ORMs
---

# Relation ORM

The **RelationORM** is used to build table of relations between other ORM objects. It works exactly like any other ORM, except that a column can also be the name of an ORM class:

```
class ProductCategoryRelation extends RelationORM {
    
    public function Definition() {
        return [
            'name' => 'product_categories',
            'column' => [
                'Product',
                'Category',
                [
                    'name' => isMainCategory',
                    'type' => 'TINYINT',
                    'default' => 0
                ]
            ]
        ];
    }
    
}
```

This table will have 3 columns: **product\_id**, **column\_id** and isMainCategory.  The **primary** key will be the ORM columns combined.
