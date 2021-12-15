---
description: Generate tables from specification
---

# DBGen

**DBGen** is a feature that lets you store the definition of one or multiple tables in a JSON file and then easily re-create those tables with a single line. Example:

```
[
   {
      "name": "users",
      "columns": [
        {
            "name": "ID",
            "type": "BIGINT",
            "notnull": true,
            "primary": true
        },
        {
           "name": "username",
           "type": "VARCHAR(300)",
           "notnull": true,
           "unique": true
        },
        {
           "name": "partner",
           "type": "BIGINT",
           "foreign": "users(ID)"
        }
      ]
   },
   {...}
]
```

```
$json = JSON::fromFile($file);

DB::create_tables($json);     // Create all
DB::create_table($json[0]);   // Create single
```
