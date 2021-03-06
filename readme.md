# Laravel Testing

- [how to create a simple laravel test][simple-test]
- [how to run php unit][run-unit]
- [what is the difference between feature and unit][fet-unit]
- [how to create a simple HTTP request][http-req]
- [how to generate fake data][gen-data]
- [how to log a laravel test][log-test]
- [how to only run a specific Dusk test?][group-tests]

## Assertions
- [assertArrayHasKey][a-arr-key]
- [assertContains][a-contains]
- [assertIsObject][a-obj]
- [assertSee][a-see]
- [assertStatus][a-status]
- [assertInputValue][a-inpt-val]


## Tabulator
- [click on the header of the table][click-tb]
- [drag a column to the right ][drag-tb]

## Database
- [check if a value is inside a database][check-db]
- [assert if a value is not in a database][no-db]

## Dusk
- [how to install dusk][inst-dusk]
- [how to make a dusk test][gen-dusk]
- [how to click on a link][click-dusk]
- [how to type in information into an input element][type-dusk]
- [how to click on the submit button from a form][click-dusk]
- [how to fill out and submit a form][fillout-dusk]
- [the different types of clicking][diff-click]
- [how to resize the browser][size-dusk]
- [how to take a screenshot][screen-dusk]
- [how to view dusk browser testing][view-testing]

[group-tests]:#how-to-group-tests
[view-testing]:#how-to-view-dusk-browser-testing
[log-test]:#how-to-log-a-laravel-test
[screen-dusk]:#how-to-take-a-screenshot
[size-dusk]:#how-to-resize-the-browser
[a-inpt-val]:assertInputValue
[drag-tb]:#drag-a-column-to-the-right
[click-tb]:#click-on-the-header-of-the-table
[no-db]:#assert-if-a-value-is-not-in-a-database
[check-db]:#check-if-a-value-is-inside-a-database
[diff-click]:#the-different-types-of-clicking
[fillout-dusk]:#how-to-fill-out-and-submit-a-form
[click-dusk]:#how-to-click-on-the-submit-button
[type-dusk]:#how-to-type-information-into-a-field
[a-contains]:#assertContains
[click-dusk]:#how-to-click-on-a-link
[gen-dusk]:#how-to-make-a-dusk-test
[a-arr-key]:#assertArrayHasKey
[a-see]:#assertSee
[a-obj]:#assertIsObject
[inst-dusk]:#how-to-install-dusk
[a-status]:#assertstatus
[gen-data]:#how-to-generate-fake-data
[http-req]:#how-to-create-a-simple-http-request
[fet-unit]:#what-is-the-difference-between-feature-and-unit
[run-unit]:#how-to-run-php-unit
[simple-test]:#how-to-create-a-simple-laravel-test
[home]:#laravel-testing



### how to group tests

<details>
<summary>
View Content
</summary>

**reference**
- [How to only run a specific Dusk test?](https://laracasts.com/discuss/channels/laravel/how-to-only-run-a-specific-dusk-test?page=1)

1. If you want to run a specific test or group a number of tests together, you can
add the `@group`  annotation before a test method.

2. Here is an example

```php
/**
 * A basic browser test example.
 * @group example
 * @return void
 */
public function testBasicExample()
{
    $this->browse(function (Browser $browser) {
        $browser->visit('/')
                ->assertSee('hello');
    });
}

/**
* @group example
*
*/
public function testRightClick(){
  $this->browse(function (Browser $browser) {
      $browser->visit('/')
              ->screenshot('see-right')
              ->assertSee('hello');
              // ->assertSee('Laravel');
  });

}
```

3. Now run in the terminal

```
php artisan dusk --group example
```

4. So two of those tests will run

</details>

[go back :house:][home]




### how to view dusk browser testing

<details>
<summary>
View Content
</summary>


1. Go to `test/DuskTestCase.php`

2. Around line **35** comment out the name `--headless`

```php
$options = (new ChromeOptions)->addArguments([
    '--disable-gpu',
    // '--headless',
    '--window-size=1920,1080',
]);
```

</details>

[go back :house:][home]


### how to log a laravel test

<details>
<summary>
View Content
</summary>

**reference**
- [Can Laravel Dusk test results be logged?](https://stackoverflow.com/questions/50742581/can-laravel-dusk-test-results-be-logged)

**Note:** --log-junit, logs the information in an **xml** format. While `--log-teamcity` logs the information in a different format

```
php artisan dusk --log-junit junit.log
php artisan dusk --log-teamcity teamcity.log
```

</details>

[go back :house:][home]


### how to take a screenshot

<details>
<summary>
View Content
</summary>

**reference**
- [How to take Browser Screenshots in Laravel Dusk](https://www.5balloons.info/how-to-take-browser-screenshots-in-laravel-dusk/)

**syntax**

`$browser->screenshot($insertName)`

#### Example
```php
$this->browse(function (Browser $browser) {

    $date = Carbon::now();
    $browser->resize(375,812)
            ->visit('/')
            ->screenshot("mobile-test")//dusk will create a screen shot called mobile-test.png
            ->assertSee('login');
});
```

</details>

[go back :house:][home]


### how to resize browser

<details>
<summary>
View Content
</summary>

**reference**
- [laravel](https://laravel.com/docs/5.6/dusk#environment-handling)

**syntax**

`$browser->resize($width,$height)`

```php
$this->browse(function (Browser $browser) {
    $browser->resize(375,812)//dusk will first resize the browser to these dimensions
            ->visit('/')
            ->screenshot("mobile-test")
            ->assertSee('login');
});
```

</details>

[go back :house:][home]

### assertInputValue

<details>
<summary>
View Content
</summary>

**reference**
- [laravel](https://laravel.com/docs/5.6/dusk#assert-input-value)

**syntax**

`$browser->assertInputValue($field, $value)`

**Note:** this is a special function only used in Dusk

```php
$this->browse(function (Browser $browser) {
    $browser->visit('/')
            ->clickLink('sign up')
            ->type("name", "jermaine")
            ->assertInputValue("name","jermaine");// will return true if dusk sees the name inside
});
```

</details>

[go back :house:][home]

### drag a column to the right

<details>
<summary>
View Content
</summary>

**reference**
- [using the mouse](https://laravel.com/docs/5.6/dusk#using-the-mouse)

**Overview:** If you want to move the tabulator column to the right, you would use the **dusk** method
`$browser->dragRight($selector, $number)`. But, to check if the width has changed when you
used the method you would have to use one of the methods from PHPUnit's Assertions

#### What is happening?

1. Dusk visits the `/table` url
2. Dusk asserts that it sees the selector `#example-table`
3. Dusk waits for the selector `.tabulator-cell` to appear
4. Dusk returns a value into **$oldWidth** from a style attribute that is from the selector **$idTitle**
5. Dusk drags the selector **$idColHandle**, to the right 10px
6. Dusk returns a value into **$newWidth** from a style attribute that is from the selector **$idTitle**
7. We use the assertion class to call the `assertNotEquals($expected, $actual)`, in order to prove
the style values have changed because you have dragged the column to the right


```php
public function testDragCol()
{
  $this->browse(function (Browser $browser) {
    $idTitle =".tabulator-col.tabulator-sortable[tabulator-field='id'] ";
    $idColHandle =".tabulator-col.tabulator-sortable[tabulator-field='id'] .tabulator-col-resize-handle";


      $oldWidth =  
            $browser->visit('/table') //1
            ->assertPresent("#example-table")//2
            ->waitFor(".tabulator-cell")//3
            ->attribute($idTitle, "style");//4



        $newWidth = $browser->dragRight($idColHandle,10)//5
            ->attribute($idTitle, "style");//6


            Assert::assertNotEquals($oldWidth, $newWidth);//7


  });
}
```

</details>

[go back :house:][home]


### click on the header of the table

<details>
<summary>
View Content
</summary>

This is one of the ways you can use dusk to click on header column in tabulator to
rearrange the order of the rows.


#### What is happening

1. You visit the home page
2. Dusk clicks on a link that says table
3. Dusk checks to see if there is a `#example-table` selector on the page
4. Dusk checks to see if the value of **1** is in the first row of the table
5. Dusk checks to see if the text "Id" is inside the selector
6. Dusk clicks on the selector within variable **$idTitle**
7. Dusk clicks on the selector again  within variable **$idTitle**
8. Dusk checks to see if it doesn't see the value 1 in the first row


```php
$this->browse(function (Browser $browser) {

  $firstRow = ".tabulator-table  .tabulator-row:first-child .tabulator-cell[tabulator-field='id']";
  $idTitle =".tabulator-col.tabulator-sortable[tabulator-field='id'] ";

    $browser->visit('/')
            ->assertSee('hello world')
            ->clickLink("table")
            ->assertPresent("#example-table")
            ->waitFor(".tabulator-cell")
            ->assertSeeIn($firstRow,1)
            ->assertSeeIn($idTitle,"Id")
            ->click($idTitle)
            ->click($idTitle)
            ->assertDontSeeIn($firstRow,1);
});
}

```

</details>

[go back :house:][home]


### assert if a value is not in a database

<details>
<summary>
View Content
</summary>

**reference**
- [laravel](https://laravel.com/docs/5.8/database-testing)

```php
public function testExample()
{
  //if the sodas table have these values for a specific row, then it will assert true
  $this->assertDatabaseHas("sodas",[
    "name" => "Product - #7465",
  "company" =>  "mountain dew"
  ]);
}
}

```

</details>

[go back :house:][home]


### check if a value is inside a database

<details>
<summary>
View Content
</summary>

**reference**
- [laravel](https://laravel.com/docs/5.8/database-testing)

**syntax**

`$this->assertDatabaseHas($table, $array)`

```php
public function testExample()
{
  //if the sodas table have these values for a specific row, then it will assert true
  $this->assertDatabaseHas("sodas",[
    "name" => "Product - #7465",
  "company" =>  "mountain dew"
  ]);
}
}
```

</details>

[go back :house:][home]


### The different types of clicking

<details>
<summary>
View Content
</summary>

There are three different types of clicking that I've seen thus far, and that is
**clickLink**, **click**, and **press**.

**reference**
- [laravel](https://laravel.com/docs/5.6/dusk#using-forms)

<details>
<summary>
With clickLink
</summary>

The **clickLink** method finds any link that has the text inserted into the parameter

**syntax**

`$browser->clickLink($linkText);`

**In testing file**

```php
$browser->visit('/')
        ->clickLink('sign up')// this will find the link that says sign up
        ->type("username", "jermaine")
        ->click(".btn.btn-primary")
         ->assertSee("skivac3@gmail.com");

```

**In the homepage**

```html
<nav class="nav">
<li class="nav-item">
  <a class="nav-link active" href="/">home</a>
</li>
<li class="nav-item">
  <a class="nav-link active" href="#">login</a>
</li>
<li class="nav-item">
  <a class="nav-link active" href="/signup">sign up</a><!-- dusk will find this link and click it -->
</li>
</nav>
```

</details>
<details>
<summary>
With click
</summary>

With click, there are two ways to get dusk to click on a specific element. One
method is to enter the selector that you want to be clicked. And the second way
is to create a dusk selector in the view



**In the test file**

```php
$browser->visit('/')
        ->clickLink('sign up')
        ->type("username", "jermaine")
        ->click(".btn.btn-primary")// this will find the selector on the page and click it
         ->assertSee("skivac3@gmail.com");

```

**In the view**

```html
...

<div class="form-group row flex-column">
  <label for="">Email</label>
  <input  class="form-control col-4" type="email" name="email" value="">
</div>
<div class="form-group row">
  <input  class="btn btn-primary" type="submit"  value="Submit"><!-- this is what dusk clicks on -->
</div>
</form>
```

### While using the dusk selector

**In the test file**

```php
$browser->visit('/')
        ->clickLink('sign up')
        ->type("username", "jermaine")
        ->click("@submit-btn")// this is the dusk selector
         ->assertSee("skivac3@gmail.com");

```

**In the view**

```html
...

<div class="form-group row flex-column">
  <label for="">Email</label>
  <input  class="form-control col-4" type="email" name="email" value="">
</div>
<div class="form-group row">
  <input  dusk="submit-btn" class="btn btn-primary" type="submit"  value="Submit"><!-- this is what dusk clicks on -->
</div>
</form>
```


</details>

<details>
<summary>
With press
</summary>

Finds the name of a button and presses it

**syntax**

`$browser->press(btnText)`

**In the test file**

```php
$browser->visit('/')
        ->clickLink('sign up')
        ->type("username", "jermaine")
        ->type("email", "skivac3@gmail.com")
        ->type("password", "password")
        ->press("Submit") // finds a button that says submit and presses it
        ->assertSee("skivac3@gmail.com");
```

**In the view**

```html
<div class="form-group row flex-column">
  <label for="">Email</label>
  <input  class="form-control col-4" type="email" name="email" value="">
</div>
<div class="form-group row">
  <input  dusk="submit-btn" class="btn btn-primary" type="submit"  value="Submit"><!-- this is what dusk clicks on -->
</div>
</form>
```

</details>



</details>

[go back :house:][home]



### how to fill out and submit a form

<details>
<summary>
View Content
</summary>


### What is happening?
1. Once dusk starts it visists the Homepage
2. Click on the "sign up" link
3. Type in the values to the username,email, and password field
4. Clicks on the submit button
5. In the controller it returns the email, and dusk is checking if they see this value


**In LoginTest**

```php
public function testExample()
{
        $browser->visit('/')
                ->clickLink('sign up')
                ->type("username", "jermaine")
                ->type("email", "skivac3@gmail.com")
                ->type("password", "password")
                ->click(".btn.btn-primary")
                ->assertSee("skivac3@gmail.com");
    });
}
}
```

**In signup.blade**

```html
<form class="" action="" method="post">
  @csrf
  <div class="form-group row flex-column">
    <label for="">Username</label>
    <input  class="form-control col-4" type="text" name="username" value=""><!-- dusk types in this field -->
  </div>
  <div class="form-group row flex-column">
    <label for="">Password</label>
    <input  class="form-control col-4" type="text" name="password" value=""><!-- dusk types in this field -->
  </div>
  <div class="form-group row flex-column">
    <label for="">Email</label>
    <input  class="form-control col-4" type="email" name="email" value=""><!-- dusk types in this field -->
  </div>
  <div class="form-group row">
    <input  class="btn btn-primary" type="submit"  value="Submit"><!-- dusk click on this button -->
  </div>
</form>
```
**In LoginController**

```php
public function createUser(Request $req){


  return $req->email; // returns the email "skivac3@gmail.com"
}
```

</details>

[go back :house:][home]


### how to click on the submit button

<details>
<summary>
View Content
</summary>

**reference**
- [laravel](https://laravel.com/docs/5.6/dusk#clicking-links)

**syntax**
`$browser->click(selector)`

The click method finds the selector within the page and clicks on the element

**In LoginTest**

```php
public function testExample()
{
    $this->browse(function (Browser $browser) {
        $browser->visit('/')// visits homepage
                ->clickLink('sign up')// clicks signup link
                ->type("username", "jermaine")//types my into the username field
                ->click(".btn.btn-primary");// finds a select that has '.btn.btn-primary' and clicks it
    });
}
}
```

**In signup.blade**

```html
<form class="" action="" method="post">
  @csrf
  <div class="form-group row flex-column">
    <label for="">Username</label>
    <input  class="form-control col-4" type="text" name="username" value="">
  </div>
  <div class="form-group row flex-column">
    <label for="">Password</label>
    <input  class="form-control col-4" type="text" name="password" value="">
  </div>
  <div class="form-group row flex-column">
    <label for="">Email</label>
    <input  class="form-control col-4" type="email" name="email" value="">
  </div>
  <div class="form-group row">
    <input  class="btn btn-primary" type="submit"  value="Submit"><!-- this is the button you will click -->
  </div>
</form>
```

</details>

[go back :house:][home]

### how to type information into a field

<details>
<summary>
View Content
</summary>

**syntax**
`$browser->type(fieldName, textValue)`

The type method will insert text into an input field and also a textarea. It can
type the proper information in by locating the name of the field

**In ProductTest**
```php
public function testExample()
{
    $this->browse(function (Browser $browser) {
        $browser->visit('/') // visits the homepage
                ->clickLink('sign up') // click the sign up link
                ->type("username", "jermaine") // inserts my name into input field
                ->assertInputValue("username", "jermaine");//checks to see if my name is inside the username field
    });
}
```

**In signup.blade**

```html
<form class="" action="" method="post">
  @csrf
  <div class="form-group row flex-column">
    <label for="">Username</label>
    <input  class="form-control col-4" type="text" name="username" value=""><!-- inserts information into this field -->
  </div>
  <div class="form-group row flex-column">
    <label for="">Password</label>
    <input  class="form-control col-4" type="text" name="password" value="">
  </div>
  <div class="form-group row flex-column">
    <label for="">Email</label>
    <input  class="form-control col-4" type="email" name="email" value="">
  </div>
  <div class="form-group row">
    <input  class="btn btn-primary" type="submit"  value="Submit">
  </div>
</form>
```


</details>

[go back :house:][home]



### assertContains

<details>
<summary>
View Content
</summary>

**reference**
- [phpunit](https://phpunit.readthedocs.io/en/8.2/assertions.html#assertcontains)

`assertContains(valueInArray,Array);`

This assertion looks for the element within an array, and if you have an associative
array it searches through the value of the array.

<details>
<summary>
Example 1
</summary>

**In ProductController**

```php
public function show($id)
{
    $soda = Soda::find($id)->toArray();
    return $soda;// this will return an object for some reason
}
```

**In ProductTest**

```php
public function testExample()
{
   $response = $this->get("/products/1");

   $arr = (array) $response;//converts into an array
   $this->assertContains("mountain dew",$arr); // this will return failure, even though the value is in the array
}

```
</details>


<details>
<summary>
Example 2
</summary>

**In ProductController**

```php
public function show($id)
{
    $soda = Soda::find($id)->toArray();
    return $soda;// this will return an object for some reason
}
```

**In ProductTest**

```php
public function testExample()
{
  // this will return failure because it does not search for a key in an associative array
  $this->assertContains("name",["company" => "mountain dew", "id" => "1", "name" =>"product"]);
}

```

</details>


<details>
<summary>
Example 3
</summary>

**In ProductController**

```php
public function show($id)
{
    $soda = Soda::find($id)->toArray();
    return $soda;// this will return an object for some reason
}
```

**In ProductTest**

```php
public function testExample()
{
  // this will return true because this a value
  $this->assertContains("mountain dew",["company" => "mountain dew", "id" => "1", "name" =>"product"]);
}

```
</details>



</details>

[go back :house:][home]


### how to click a link

<details>
<summary>
View Content
</summary>


**In LoginTest**

```php


namespace Tests\Browser;

use Tests\DuskTestCase;
use Laravel\Dusk\Browser;
use Illuminate\Foundation\Testing\DatabaseMigrations;

class LoginTest extends DuskTestCase
{
    /**
     * A Dusk test example.
     *
     * @return void
     */
    public function testExample()
    {
        $this->browse(function (Browser $browser) {
            $browser->visit('/')//visits the home page
                    ->clickLink('sign up')// clicks on a link that says sign up
                    ->assertSee("Username");// and checks if there is text that says Username
        });
    }
}
```
**In Homepage**

```html
...
<header class="bg-dark d-flex justify-content-center">
  <nav class="nav">
  <li class="nav-item">
    <a class="nav-link active" href="/">home</a>
  </li>
  <li class="nav-item">
    <a class="nav-link active" href="#">login</a>
  </li>
  <li class="nav-item">
    <a class="nav-link active" href="/signup">sign up</a> <!-- dusk will find the link and click on it -->
  </li>
  <li class="nav-item">
    <a class="nav-link" href="#">facilities</a>
  </li>
  <li class="nav-item">
    <a class="nav-link" href="#">help</a>
  </li>
</ul>
</header>
...
```

**In Signup Page**

```html
@extends('layout')

@section("main")
  <section class="container">
    <form class="" action="" method="post">
      <div class="form-group row flex-column">
        <label for="">Username</label> <!-- this is the Username that dusk sees   -->
        <input  class="form-control col-4" type="text" name="username" value="">
      </div>
      <div class="form-group row flex-column">
        <label for="">Password</label>
        <input  class="form-control col-4" type="text" name="password" value="">
      </div>
      <div class="form-group row flex-column">
        <label for="">Email</label>
        <input  class="form-control col-4" type="email" name="email" value="">
      </div>
      <div class="form-group row">
        <input  class="btn btn-primary" type="submit" name="submit" value="Submit">
      </div>
</form>
  </section>
@stop

```

</details>

[go back :house:][home]



### how to make a dusk test

<details>
<summary>
View Content
</summary>


```
php artisan dusk:make  LoginTest
```

</details>

[go back :house:][home]


### assertSee

<details>
<summary>
View Content
</summary>

**reference**
- [laravel](https://laravel.com/docs/5.8/http-tests#assert-see)

**In ProductTest**

```php

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
    public function testKey()
    {
       $response = $this->get("/products/1");
       $this->assertArrayHasKey("id",$response); //returns true if id is a key value
    }
}
```

**In ProductController**

```php
public function show($id)
{
    $soda = Soda::find($id);


  return view('single-product',["soda" => $soda]);
}


```

**In view**

```php
@extends('layouts.default')
@section('main')
Product number: {{$soda->id}}
<p>Name: {{$soda->name}}</p>
<p>Company: {{$soda->company}}</p>
<p>Ounces: {{$soda->ounces}}</p>
<p>Price: {{$soda->price}}</p>

@stop

```

</details>

[go back :house:][home]


### assertArrayHasKey

<details>
<summary>
View Content
</summary>

**reference**
- [phpunit](https://phpunit.readthedocs.io/en/8.2/assertions.html#assertarrayhaskey)


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
    public function testKey()
    {
       $response = $this->get("/products/1");
       $this->assertArrayHasKey("id",$response); //returns true if id is a key value
    }
}

```
**In ProductController**

```
public function show($id)
{
    $soda = Soda::find($id)->toArray(); // transforms data into an associative array

   echo $soda;
}

```

</details>

[go back :house:][home]


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

```php
//<?php

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

```php
//<?php

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

```php

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

3. Now, this version of dusk **will only work** in chrome that has the version **70-73**.
So if you have a chrome version higher than that, then *you have to uninstall  chrome*.
So in the start menu type in "chrome", and right-click the icon to uninstall it.

4. After chrome is uninstalled, go to this [link](https://www.slimjet.com/chrome/google-chrome-old-version.php) and install a version of chrome between 70-73

5. In order to stop automatic updates of chrome, visit this [link](https://www.makeuseof.com/tag/stop-automatic-chrome-updates-windows/)

6. After that chrome version installed, add this into the terminal

```
php artisan dusk
```

7. Hopefully, the test will pass

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
