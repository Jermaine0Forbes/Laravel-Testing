# Laravel Testing

- [how to create a simple laravel test][simple-test]
- [how to run php unit][run-unit]
- [what is the difference between feature and unit][fet-unit]
- [how to create a simple HTTP request][http-req]

[http-req]:#how-to-create-a-simple-http-request
[fet-unit]:#what-is-the-difference-between-feature-and-unit
[run-unit]:#how-to-run-php-unit
[simple-test]:#how-to-create-a-simple-laravel-test
[home]:#laravel-testing


### how to create a simple http request

<details>
<summary>
View Content
</summary>



```php
namespace Tests\Feature;

use Tests\TestCase;
use Illuminate\Foundation\Testing\WithFaker;
use Illuminate\Foundation\Testing\RefreshDatabase;

class userTest extends TestCase
{
    /**
     * A basic test example.
     *
     * @return void
     */
    public function testHomepage()
    {
        $response = $this->get("/");

        $response->assertStatus(200);
}

```

</details>

[go back :house:][home]


### what is the difference between feature and unit

<details>
<summary>
View Content
</summary>

**reference**
- [How to write tests for Laravel applications](https://blog.pusher.com/tests-laravel-applications/)

**Unit Testing:** Unit testing focuses on testing the functionality of a little part of your application like a handful of methods or a class.

**Feature Testing:** Tests that an entire feature actually works. At this point, you can test many classes and methods, or an entire package depending on how your application is structured.

</details>

[go back :house:][home]



### how to run php unit

<details>
<summary>
View Content
</summary>

```
./vendor/bin/phpunit
```

</details>

[go back :house:][home]



### how to create a simple laravel test

<details>
<summary>
View Content
</summary>

**reference**
- [laravel](https://laravel.com/docs/5.8/testing)

1. Create a name for a test in the terminal

```
// Create a test in the Feature directory...
php artisan make:test UserTest


```

2. In `tests/Feature` you should find your test file and if you open it will look
like this

```php


namespace Tests\Unit;

use Tests\TestCase;
use Illuminate\Foundation\Testing\RefreshDatabase;

class ExampleTest extends TestCase
{
    /**
     * A basic test example.
     *
     * @return void
     */
    public function testBasicTest()
    {
        $this->assertTrue(true);
    }
}
```

3. To run the test you created, simply add this in the terminal

```
./vendor/bin/phpunit

```

4. This will run the tests and tell you if the number of tests have succeeded or failed


</details>

[go back :house:][home]
