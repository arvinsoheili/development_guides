1. To check a specific URI we should use: `$this->get('URI');`. we should put it in a variable, in this case we gonna use: `$response`.
2. we use: `$response->assertStatus(200);` to check if the page that we refered earlier will found or not.
3. Now we should head to our terminal and use this artisn command to start testing operation: `php artisan test`.
- In case, we want to check if the page loaded successfully or not we can use: `$response->assertSee('VALUE');`. it will check if the page contains the value you provided, or not. Or you can do quite opposite by writing: `$response->assertDontSee('VALUE');`.

So now we wanna do tests on our DB operations. but in case of doing tests on DB, we gonna be careful on our production database (we don't want to ruin the data). So we gonna make new `.env.testing` file which will make an alternative .env file special for our testing operations.

Optionally we can do this instead: open `phpunit.xml` and uncomment database instances and change them manually to match your new testing special database.

### NOTICE: we don't want our data to be deleted, so we must double check if we setup new database for testing, or ever you going to refresh your DB accidentally, and it will cause data loss on your production database.

what you gonna do now is add this line inside your test class to make a migration in you database so you can check insertion and other data operations: `use RefreshDatabase;`.

##

In testing we have to do our tests in a specific order. we name it AAA: Arrange Act Assert.
### Arrange
we will do whatever operation like adding some data to our database or we can do multiple arrange oeprations.

### Act
we should make a action like giving a url to check. Act should be only one operation.

### Assert
we can do one or more assertions, to show if the conditions passed or not.
##

- remember we got assertsee to check specific value in view, but it wouldn't work everytime for some reason. instead, we can use `assertViewHas` and pass a collection to check if there's the value is exist.
this is a step by step guide.
1. in this case we will using a pre stored data, which is product in our case.
2. we gonna use $products as the stored data which we want to check if this data are already showing in view or not.
```
$response->assertViewHas('products', function ($collection) use ($product) {
    return $collection->contains($product);
});
```

