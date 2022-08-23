# CRUD

CRUD is a term that stands for **Create-Read-Update-Delete**. It refers to the standard routes (defined by the API Restful standard) that are normally defined to manage a model/entity in our platform.

For example, imagine a platform where users post videos. The API would offer routes like these:

```
GET    /api/videos       Get list of videos
POST   /api/videos       Post a new video
GET    /api/videos/:id   Get a specific video
PUT    /api/videos/:id   Edit a video
DELETE /api/videos/:id   Delete a video
```

You could create these routes using any of the other routing methods explained previously. But a faster and cleaner method is using the **CRUD** class:

<pre class="language-php"><code class="lang-php"><strong>CRUD::instance('/api/videos')
</strong>
    // GET /api/videos
    ->list(function($req) {
        return ...
    })
    
    // POST /api/videos
    ->create(function($req) {
        return ...
    })     
    
    // GET /api/videos/:id
    ->get(function($req, $params) {
        $videoId = $params->id;
        return ...
    })         
    
    // DELETE /api/videos/:id
    ->delete(function($req, $params) {
        return ...
    })      
    
    // PUT /api/videos/:id
    ->edit(function($req, $params) {
        return ...
    })
    
    // Add routes to the Router
    ->generate();
    </code></pre>

The CRUD class defines a base URL (/api/videos), and the has these methods: **list, get, create, edit, delete**, to define the CRUD routes.

{% hint style="info" %}
Notice that there's **five of them** instead of four, that's because the READ in C**R**UD would actually correspond to two endpoints, one to get the list of items (GET /api/videos) and another one to get a specific item (GET /api/videos/:id).
{% endhint %}

### Custom routes on a CRUD

Sometimes it's also necessary to create additional features and routes on your entities. For example, imagine that users can like posted videos or add them to favorites. In that case, routes like these could serve:

<pre><code><strong>PUT/DELETE /api/videos/:id/like
</strong>PUT/DELETE /api/videos/:id/favorite</code></pre>

The CRUD class allows you to add these as **custom routes**:

```php
CRUD::instance('/api/videos')

    ->custom('PUT', '/:id/like', function($req, $params) {
        // ...
    })
    
    ->custom('DELETE', '/:id/like', function($req, $params) {
        // ...
    })
    
    ->generate();
```

The custom methods specified the **method**, the route **added to the base route of the CRUD**, and finally the action.

### Middlewares with CRUD

A CRUD can also use a middleware for its routes:

```php
CRUD::instance('/api/videos')
    ->middleware('auth')
    ->delete()        // DELETE /api/videos/:id
    ->generate();
```

It's possible, however, that different endpoints for the same entity require different middlewares or permissions. For example, imagine that unauthenticated users can see posted videos, but not create them. Then you should use two different CRUDs:

```php
CRUD::instance('/api/videos')
    ->list()        // GET/api/videos
    ->generate();

// Only for logged users
CRUD::instance('/api/videos')
    ->middleware('auth')
    ->create()        // POST /api/videos
    ->generate();
```
