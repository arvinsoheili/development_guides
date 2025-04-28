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
## Acting as a logged in user
in case that we want to test a page which requires an admin or user logged in, we gonna use `actingAs(user)`.
we wanna login as the user and begin testing. for Arrange we want to make new user/admin for our test and assign it in `$user` variable. then we going to continue our Arrange part as always
now in Act section we want to access the url. but we're going to use `actingAs` method. example:
```php
// $user is a prebuilt user that we made in Arrange section
$response = $this->actingAs($user)->get(uri);
```
now we can test the page as always.
then we can write Assert section like previous parts.

## Auth test
if we want to test authentication in specific pages we won't act as user in our new test. then what we going to do is get the test passed, by using new assert options.
in case that our unauthenticated page, redirect the user to login page we will use two new assertion options.
```php
// the first one is assert status set to 302, which indicates redirected status.
$response->asertStatus(302);
// the second option is assertRedirect. we use it to check the page that user redirected to.
$respone->assertRedirect(uri e.g.: "login);
```

### Test redirection after login
if we want to make a test that check our user will redirected to target page after login we can follow these steps.
1. first make the user/admin in Arrange section.
2. login the user in login page by doing this:
```php
$response = $this->post(uri, [
    //use the crendintials that your login needs. and remember to use the actuall data that you made the user with.
    'email' => 'user@user.com',
    'password' => 'pass1234'
]);
```
3. then, in Assert section we can use the same assertion option that we used for indicating redirections.
```php
$response->assertStatus(status: 302)
->assertRedirect(uri: 'dashboard');
```

## Private mehods or setUp()
we can avoid create same data by simply using Private methods or using setUp() in our test file.

### Private method
you can make new private function in your test class like this. for example we want to make a user record in every test instead of writing all of those codes several times, we can do this.
make a private function like this:
```php
private function createUser()
{
    // user creation codes
}
```
then you can use this in other functions like this: `$this->createUser()`

### setUp()
setup method is almose look like the private functions but you can make methods more simple.
first you want to make setUp() function:
```php
protected function serUp(): void
{
    parent::serUp(); // don't forget to add this line.

    $this->createUser =  // user creation codes.
    //then you can use $this->createUser in every other function
}
```

## Testing that data will save
 


