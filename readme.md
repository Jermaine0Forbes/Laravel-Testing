# Laravel Testing

- [how to create a simple laravel test][simple-test]
- [how to run php unit][run-unit]
- [what is the difference between feature and unit][fet-unit]
- [how to create a simple HTTP request][http-req]
- [how to generate fake data][gen-data]

[gen-data]:#how-to-generate-fake-data
[http-req]:#how-to-create-a-simple-http-request
[fet-unit]:#what-is-the-difference-between-feature-and-unit
[run-unit]:#how-to-run-php-unit
[simple-test]:#how-to-create-a-simple-laravel-test
[home]:#laravel-testing



### How to generate fake data

1. create a factory model, also make sure that you have the database
and model created

```
php artisan make:factory Article
```

2. If you have not created a model or the table then type the command in


```

php artisan make:model  Article -m  // this creates the model and the migration table

```


3. In `databases/migrations` find the migrations table and edit it to your liking

```
<?php

use Illuminate\Support\Facades\Schema;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateSodasTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('articles', function (Blueprint $table) {
            $table->increments('id');
            $table->string("title", "50");
            $table->text("content");
            $table->integer("author_id");
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('articles');
    }
}


```

4. Migrate the table

```
 php artisan migrate
```

5. then go to `databases\factories\Article.php`, and add the faker property

```
<?php

use Faker\Generator as Faker;
use App\Article;

$factory->define(Article::class, function (Faker $faker) {
     return [
        'title' => $faker->title,
        'content' => $faker->paragraph,
        'author_id' => $faker->randomDigit
    ];
});
```

6. then go to `databases\seeds\DatabaseSeeder.php` and add the code to the
method

```
<?php

use Illuminate\Database\Seeder;
use App\Article;

class DatabaseSeeder extends Seeder
{
    /**
     * Run the database seeds.
     *
     * @return void
     */
    public function run()
    {
        // $this->call(UsersTableSeeder::class);
        factory(Article::class,1000)->create();
    }
}

```

7. finally, seed the data

```
php artisan db:seed

```

8. And that will create the rows of data

[go back :house:][home]

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
