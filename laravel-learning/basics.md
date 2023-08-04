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


