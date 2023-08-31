# Requests

### 1.get

### 2.POST
 
### 3.DELETE

there's no delete action in html so we need to fake it by set the method `POST` in forms. then type `@csrf` & `@method(DELETE)`.

go to your route file type a new route:

```
route::delete('route/{id}', 'nameController@destroy)
```

go to your controller, type: 
 
```
public function destroy {
    //find your db 
    $var -> delete();
    //you can redirect if you want
}
```

