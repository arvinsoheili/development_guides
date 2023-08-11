# Controllers

### 1.Get started with controllers

at first you need to create a controller.

to do this you should open your therminal and type:
```
php artisan make:controller controllername
```
now a file named `controllername` created in `app/HTTP/controller/controllername.php`.

in this file you have some codes under them you got a opend `{}` and you need to define your route functions in it:

```
public function name() {
  function ingredients
}
```
now you should go back to your routes and replace the second parameters of routes with `'controllername@name'`.
