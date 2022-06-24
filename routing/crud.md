# CRUD

CRUD stands for Create-Read-Update-Delete. It refers to the standard routes (defined by the API Rest) used to manage a model/entity.

For example, imagine a platform where users post videos, then the API would offer these routes:

```
GET    /api/videos       Get list of videos
POST   /api/videos       Post a new video
GET    /api/videos/:id   Get a specific video
PUT    /api/videos/:id   Edit a video
DELETE /api/videos/:id   Delete a video
```

You could create these routes using any of the routing methods explained previously. But a faster method is using the **CRUD** class:

```
$crud = new CRUD('/base');

// or
CRUD::instance('/api/videos')
    ->list(function($req) {  // GET /api/videos
        return ...
    })
    ->create(function($req) {  // POST /api/videos
        return ...
    })     
    ->get(function($req, $params) {   // GET /api/videos/:id
        $videoId = $params['id'];
        return ...
    })         
    ->delete(function($req, $params) { // DELETE /api/videos/:id
        return ...
    })      
    ->edit(function($req, $params) {   // PUT /api/videos/:id
        return ...
    })
    
    ->generate();   // Create the routes
    
```

The CRUD class allows you to define these CRUD routes in a very quick and agile way.

### Middlewares with CRUD

A CRUD can also use a middleware for its routes:

```
CRUD::instance('/api/videos')
    ->middleware('auth')
    ->delete()        // DELETE /api/videos/:id
    ->generate();
```

It's possible, however, that different endpoints for the same entity require different middlewares / permissions. For example, imagine that unauthenticated users can see posted videos, but not create them. Then you should use two different CRUDs:

```
CRUD::instance('/api/videos')
    ->list()        // GET/api/videos
    ->generate();

// Only for logged users
CRUD::instance('/api/videos')
    ->middleware('auth')
    ->create()        // POST /api/videos
    ->generate();
```

### Custom routes on a CRUD

Sometimes it's also necessary to create additional features and routes on your entities. For example, imagine users can like posted videos or add them to favorites. In that case, routes like these could serve:

```
/api/videos/:id/like
/api/videos/:id/favorite
```

The CRUD class allows you to add these as **custom routes**:

```
CRUD::instance('/api/videos')
    ->custom('POST', '/:id/like', function($req, $params) {
        $videoId = $params['id'];
    });
```
