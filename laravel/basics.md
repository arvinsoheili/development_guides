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


<p>{{ $key1 }} {{ $key2 }}<p/> // how to return the value in html template
```

#### II.`@if` statment

you can use it like php in the html template but type `@if`, `@else`, `@elseif` instead of `if, else, elseif`.

 Note: you can use php by start it with `@php` and close it by `@endphp` when we finished.

#### III.`@for` statment

you can use `@for` statment like `for` loop in php. you can start it with `@for` and close it by `@endfor`. 

#### IV.`@foreach` loop

you can open the loop by `@foreach` and close it by `@endforeach`.

```
$var = ['key1' => 'value1', 'key2' => 'value2'] //in routes file

@foreach($var as $etc)
  <p>{{ $etc['key1] }} - {{ $etc['key2'] }}</p> //in blade file
@endforeach
```
##

### 3.layout files

so if want to have the same header, footer or ... in all pages we need to have layout files.

#### steps:

1.create a folder named `layouts` in `views` directory.

2.create file named `layout.blade.php`.

3.now you need to cut your header and footer or every parts that are same in every file and paste it in layout file.

4.go to your views and paste the code below to top of every blade file:

```
@extends('layouts.layout')
```
5.at the beggining of your code paste `@section('your custom name)` and close it by `@endsection` at the end of your codes.

6.now go to layout file and paste `@yield('your entered name')` between your header and footer.

##

### 4.adding external css and image

- in public dir we got a folder names `css` and you need to craete a folder named `img` for images.

#### I.css

2.to include a css file you sould create a `css` named anything like `styles.css` file in `public/css`. in layout file we give the address like:

```
<link href="/css/styles.css" rel="stylesheet">
```
NOTE: laravel recognize the file dir like this theres no need to give address like this: `public/css/styles.css`.

#### II.image

 1.put your image files in img folder.

 2.in your code open a img tag and fill it like below:
 ```
 <img src="/img/img.jpg" alt="">
  ```
##

### 5.query parameters

#### site.com/article?name=arvin
the `?name=arvin` is a query parameter that when we use it in laravel we can show it in our page.

query parameter is a request method that we can type it in routes to show it in our page.
```
//in web.php
Route::get('/', function () {
    return view('welcome', [
    'variable' => request('var'),
    'name' => request('name')
  ]);
});

//in .blade.php files
<p> {{ $var }}</p>
<p>{{ $name }}</p>
```
##

### 6.Route Parameters (Wildcards)

#### site.com/article/`2`
the highlighted number is the wildcard.

we can use wildcards to show a product page or anithing else.

1.we sould type the route lik below:
```
Route::get('/{id} ', function ($id) { //you can type anything instead of id
   return view('details', ['id' => $id]);
});
```

2.now you need to create a file named `details.blade.php` and make it your wildcard page.

3.now type `{{ $id }}` in any tag you want to show the wildcard value in the page 
#

# POST Request

we use post request to sent or post some data to databases.
to do this we need to create a form in html and set `action` and `method` to `/redirectaddress` and `POST`.
#### example: 
```
<form action='/index' mathod='POST` >
```
### Handling a POST request

1.create a new route in your routes file:
```
route::post('/index', 'NameController@store');
```

2.Now go to your controller file and create function for your route:

```
public function  store() {

return redirect('/');
}
```
NOTE: if you fill and submit your form you will end to a error page to prevent this problem you should paste `@csrf` under your form tag.

3.now you gonna access to your database tables with `request('colname')`. you should put it in new array :
```
$var = new Var();

$var->colname = request('colname');
```

4.to save the changes in your database add `$var->save();` at the end.
