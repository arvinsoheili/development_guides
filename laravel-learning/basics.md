# laravel basics

### 1.Routes & Views

- when a user type a address in browser, will send a request to host that using `laravel` as backend.
  
- then routes file (`web.php`) decides what to do by using "`route` class" and "`get` method" that takes two parameters:

  (`'the route that we expct like (/articles)' , function() {}`).

- the route will look like:

 ```
  Route::get('/', function () {
    return view('welcome');
  });
 ```
  
- now it'll return a `HTML Template` by using `VIEW` method thet takes a parameter as string that is the name of the `HTML` file in `/views` folder. the file is like: ` welcome.blade.php`. laravel only takes the first part of file name as a string

-> Note: remember that `blade` is a template engine

api routes resource routes
##

### 2.Blade sintax

#### I.database values

if you want to use a value from DB instead of using a plain string, you need to type the `key` in `{{}}`:
```
['key1' => 'value1', 'key2' => 'value2'] // our database example
```
```
<p>{{ $key1 }} {{ $key2 }}<p/> // how to return the value in html template
```

#### II.`@if` statment

you can use it like php in the html template but type `@if`, `@else`, `@elseif` instead of `if, else, elseif`.

#### Note: you can use php by start it with `@php` and close it by `@endphp` when we finished.


