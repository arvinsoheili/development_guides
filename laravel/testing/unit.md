in unit testing we test our inner code functionalities to check if they're working fine or there is bug or error in process.
tests on units are located in test/unit directory. 
they are almost similar to feature tests on naming functions and some other entities.
##
### test an expected value
we do this test on functions that calculates or creating new things, `we use assertEquals`. in this case we imagine there is a currency convertor service in our app.
```php
$this->assertEquals(ExpectedValue, TargetFunction);
// example
$this->assertEquals(98, (new CurrencyService())->convert(100, 'usd', 'eur)); // these are not actuall values they are using for testing purposes.
// function structure is this: convert(amount, currencyFrom, currencyTo);
```
