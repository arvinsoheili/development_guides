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

open your controller file. locate your route, there is few ways to intract with your model.

- retrive all of your data and pass it to a view:
  ```
  $something = modelname::all();

  return view('pagename', 
