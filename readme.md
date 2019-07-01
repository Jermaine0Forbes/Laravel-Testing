# Laravel Testing

- [how to create a simple laravel test][simple-test]
- [how to run php unit][run-unit]
- [what is the difference between feature and unit][fet-unit]
- [how to create a simple HTTP request][http-req]
- [how to generate fake data][gen-data]

## Assertions
- [assertStatus][a-status]
- assertSee
- assertContains
- assertArrayHasKey
- [assertIsObject][a-obj]

## Dusk
- [how to install dusk][inst-dusk]

[a-obj]:#assertIsObject
[inst-dusk]:#how-to-install-dusk
[a-status]:#assertstatus
[gen-data]:#how-to-generate-fake-data
[http-req]:#how-to-create-a-simple-http-request
[fet-unit]:#what-is-the-difference-between-feature-and-unit
[run-unit]:#how-to-run-php-unit
[simple-test]:#how-to-create-a-simple-laravel-test
[home]:#laravel-testing

### assertIsObject

<details>
<summary>
View Content
</summary>

**reference**
- [phpunit](https://phpunit.readthedocs.io/en/8.2/assertions.html#assertisobject)

If you are just checking information and echoing out the information
in an object **assertIsObject** this is the best way to check if it is an object

**In ProductTest**

```
<?php

namespace Tests\Unit;

use Tests\TestCase;
use Illuminate\Foundation\Testing\WithFaker;
use Illuminate\Foundation\Testing\RefreshDatabase;

class ProductTest extends TestCase
{
    /**
     * A basic test example.
     *
     * @return void
     */
    public function testExample()
    {
       $response = $this->get("/products/1");

       $this->assertIsObject($response); // this will return true
       $response->assertSee('"id"'); // this will return false even though id is within the object
    }
}



```


**In the controller**

```
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Soda as Soda;

class ProductController extends Controller
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
     public function show($id)
     {
         $soda = Soda::find($id);

       echo $soda; // outputs the object
     }
}
```

**In routes**

```

Route::prefix("products")->group(function(){
  Route::get('/', "ProductController@index");
  Route::get('{id}', "ProductController@show");// grabs the id of the product
});

```




</details>

[go back :house:][home]


### how to install dusk

<details>
<summary>
View Content
</summary>

**reference**
- [laravel](https://laravel.com/docs/5.6/dusk)

**This is how you install laravel dusk in laravel 5.6**

1. Install `laravel/dusk`

```
composer require --dev laravel/dusk:"^4.0"
```

2. Then install dusk with php artisan

```
php artisan dusk:install
```

3. Now, this version of dusk will only work in chrome that has the version 70-73.
So if you have a chrome version higher than that, then you have to uninstall  chrome.
So in the start menu type in "chrome", and right-click the icon to uninstall it.

4. After chrome is uninstalled, go to this [link](https://www.slimjet.com/chrome/google-chrome-old-version.php) and install a version of chrome between 70-73

5. After that chrome version installed, add this into the terminal

```
php artisan dusk
```

6. Hopefully, the test will pass

</details>

[go back :house:][home]

### assertStatus

<details>
<summary>
View Content
</summary>

**reference**
- [laravel](https://laravel.com/docs/5.8/http-tests#assert-status)


```
$response->assertStatus($code);
```

</details>

[go back :house:][home]


### How to generate fake data


<details>
<summary>
View Content
</summary>


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

</details>

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
