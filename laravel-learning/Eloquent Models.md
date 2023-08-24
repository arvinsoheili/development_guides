# Eloquent Model

after you create your database with migration you need to add some data and if you wonder show it in your page.

### 1.add some record to your DB.

### 2.make a Eloquent model.

open your therminal, type:
```
php artisan make:model modelname
```
laravel will create a file in `app` dir in your root dir.

### 3.Intract with model

open your controller file. type `use App\filename-without-format` before the routes functions.

locate your route, there is few ways to intract with your model.

- retrive all of your data and pass it to a view:
  
  ```
  $variable = modelname::all();

  return view('pagename', [ 'key' => $variable ]);
  ```

- retrive all of your data, order it and pass it to view:

  ```
  $variable = modelname::orderBy('colname', 'asc/desc')->get(); 
  ```
  NOTE: the get() method is very important unless you dont want to show it in your page.

- retrive and pass the items that you filter it.

  ```
  $variable = modelname::where('colname', 'value')->get();
  ```
  

  
  
