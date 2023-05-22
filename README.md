<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

<p align="center">
<a href="https://github.com/laravel/framework/actions"><img src="https://github.com/laravel/framework/workflows/tests/badge.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

## About Laravel

Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable and creative experience to be truly fulfilling. Laravel takes the pain out of development by easing common tasks used in many web projects, such as:

Certainly, here's a suggested roadmap for learning Laravel:

-   Basics of PHP: Before you start with Laravel, make sure you have a solid understanding of PHP. You should be familiar with basic programming concepts, such as variables, functions, control structures, and object-oriented programming.

-   Composer: Learn how to use Composer, which is a dependency manager for PHP. Composer is used to install Laravel and its dependencies.

-   Laravel installation: Install Laravel using Composer. You can use the Laravel installer or create a new project manually.

-   Routing: Learn how to create routes in Laravel. Routes are used to map URLs to controller methods.

-   Migrations: learn how to create, modify, and delete database tables and their columns.

-   Models: Learn how to create models in Laravel to interact with your database.

-   Seeding: Learn how to create seeders and populate your database with dummy data.

-   Controllers: Learn how to create controllers in Laravel. Controllers are responsible for handling requests and returning responses.

-   Views: Learn how to create views in Laravel. Views are used to generate HTML output.

-   Blade templating engine: Learn how to use Blade, which is a templating engine used by Laravel. Blade makes it easy to create reusable templates.

-   Eloquent ORM: Learn how to use Eloquent, which is an Object-Relational Mapping (ORM) system used by Laravel. Eloquent makes it easy to work with databases and create database models.

-   Middleware: Learn how to use middleware in Laravel. Middleware is used to intercept HTTP requests and perform actions before or after the request is handled by a controller.

-   Authentication: Learn how to implement user authentication in Laravel. Laravel provides built-in authentication features that can be easily customized.

-   Testing: Learn how to write tests in Laravel. Laravel provides a testing framework that makes it easy to write and run tests.

-   Advanced topics: Once you are comfortable with the basics of Laravel, you can start learning more advanced topics such as API development, queues, broadcasting, events, and notifications.

## Routing

1. Basic Routes: Basic routes are the most common type of route in Laravel. They define the URI and the corresponding closure that should be executed when the route is accessed. Here's an example:

```
Route::get('/hello', function () {
    return 'Hello, World!';
});
```

2. Route Parameters: You can define route parameters to capture segments of the URI. The parameters are passed to the closure as arguments. Here's an example:

```
Route::get('/users/{id}',function($id){
    return ('user ID is : '.$id);
});
```

3. Optional Parameters: You can define optional parameters by wrapping them in curly braces and making them optional with a question mark. Here's an example:

```
Route::get('/users/{id?},function($id = null){
    return('user ID is :'.$id);
});
```

4. Named Routes: You can give a route a name to make it easier to reference in your code. Here's an example:

```
Route::get('/users/{id?}', function($id = null)
{
    return('user ID is :'.$id);
})->name('users.show');
```

5. Route Groups: You can group several routes together and apply middleware or other attributes to the entire group. Here's an example:

```
Route::middleware(['auth'])->group(function(){
    Route:get('/dashboard', function(){
        return view('dashboard');
    });

    Route:get('/profile',function(){
        return view('profile');
    });
})
```

6. Route Prefixes: You can add a common prefix to a group of routes. Here's an example:

```
Route::prefix('dashboard')->group(function(){
    route::get('/student', function(){
        return view('student');
    });
    route::get('/staff', function(){
        return view('staff');
    });
});
```

7. Route Middleware: You can apply middleware to a single route or a group of routes. Here's an example:

```
Route::get('/archive', function(){
    return view('archive');
})->middleware(['auth']);
```

8. Route Caching: You can cache your routes to improve the performance of your application. Here's how to cache your routes:

```
php artisan route:cache
```

## Migrations

1. In Laravel, migrations and models are key components of the database management system provided by the framework. Migrations allow you to create and modify database tables, while models provide an object-oriented interface to interact with the database tables.

2. Migrations are used to create, modify, and delete database tables and their columns.

3. Migrations are defined as classes and stored in the database/migrations directory of your Laravel project.

4. Each migration class has two essential methods: **up()** and **down()**.

* The **up()** method defines the changes you want to make to the database schema, such as creating tables or adding columns.

* The **down()** method specifies how to revert those changes if needed.

5. Inside the migration class, you can use various schema builder methods provided by Laravel to define the structure of your database tables.

6. Once you've defined your migration, you can run it using the migrate Artisan command, which will execute all pending migrations and update the database schema accordingly.

7. Laravel keeps track of which migrations have been executed, allowing you to roll back migrations using the migrate:rollback command.

**Example:**

* Create migration categories and products

```
docker-compose exec myapp php artisan make:migration create_categories_table
```

```
docker-compose exec myapp php artisan make:migration create_products_table
```

* table categories :
```
    public function up(): void
{
    Schema::create('categories', function (Blueprint $table) {
        $table->id();
        $table->string('name');
        $table->string('description');
        $table->boolean('active')->default(true);
        $table->string('reference')->unique();
        $table->string('icon');
        $table->timestamps();
    });
}
```

* table products :
```
    public function up(): void
    {
        Schema::create('products', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('description');
            $table->boolean('active')->default(true);
            $table->string('image');
            $table->decimal('price',8,2);
            $table->integer('stock');
            $table->unsignedBigInteger('category_id');
            $table->timestamps();
            $table->foreign('category_id')->references('id')->on('categories');
        });
    }
```
**id:** Auto-incrementing primary key.

**name:** String column to store the product name.

**price:** Decimal column to store the product price, with 8 total digits and 2 decimal places.

**active:** Boolean column to indicate if the product is active or not, defaulting to true.

**category_id:** Unsigned big integer column to store the foreign key referencing the id column of the categories table.

**timestamps():** Creates created_at and updated_at columns for tracking record creation and modification timestamps.

The foreign key constraint is added to the category_id column, referencing the id column of the categories table.


**Example 2:**

```

Schema::create('class', function (Blueprint $table) {
    $table->id();
    $table->string('code');
    $table->string('secteur');
    $table->string('number_students');
    $table->timestamps();
 });

```

```
Schema::create('students', function (Blueprint $table) {
    $table->id();
    $table->string('name');
    $table->string('cnie');
    $table->date('birth_date');
    $table->string('profile');
    $table->string('adress');
    $table->string('city');
    $table->decimal('zip_code');
    $table->unsignedBigInteger('class_id');
    $table->timestamps();
    $table->foreign('class_id')->references('id')->on('class');
});
```



## Models

models are used to interact with your database tables. They represent the data and business logic of your application. Models allow you to perform database operations such as retrieving records, creating new records, updating existing records, and deleting records.

1. To create a model in Laravel, you can use the php artisan command-line tool or manually create a new file. Here are the steps:

        php artisan make:model `your_model`

    This will create a `your_model` model file in the app directory.
2. Manual Creation:

        <?php

        namespace App;

        use Illuminate\Database\Eloquent\Model;

        class your_model extends Model
        {
            // Model logic and attributes
        }
        
    In the `your_model` class, you can define relationships with other models, specify table names, define guarded or fillable attributes, and add custom methods for handling specific business logic.


**Example:**

        protected $fillable = [
                'name',
                'cnie',
                'birth_date',
                'profile',
                'adress',
                'city',
                'zip_code',
                'class_id',
            ];


## Seeding

seeders are used to populate your database with sample or test data. Seeders allow you to define data in a structured way and insert it into your database tables using the Laravel's database seeding feature.

To create a seeder in Laravel, you can follow these steps:

1. Generate a Seeder:

    Run the following command in your terminal to generate a new seeder file:

        php artisan make:seeder StudentSeeder

    This command will create a new seeder file named StudentSeeder in the database/seeders directory.

2. Define the Seeder Class:


    Open the generated StudentSeeder file and define the class as follows:

        <?php

        namespace Database\Seeders;

        use Illuminate\Database\Seeder;
        use App\Models\Student; // Required !!!!!!!!!!!!!!!!

        class StudentSeeder extends Seeder
        {
            public function run()
            {
                // Seed your database here
            }
        }

    In the run() method, you can write the code to insert data into your database tables.

3. Insert Data in the Seeder:

    Within the run() method of the seeder, you can use Eloquent model methods or raw SQL queries to insert data into your tables. Here's an example of inserting a student record using the Student model:

         public function run()
        {
            students::create([
            'name' => 'Othmane elkhiari',
            'cnie' => 'Q3xxxx',
            'birth_date' => '2003-11-28',
            'profile' => 'https://cdn.intra.42.fr/users/d1950c2fdfef811df79ec1f87f7431f5/oelkhiar.jpg',
            'address' => '28 Lot salam',
            'city' => 'Boujniba',
            'zip_code' => '25100',
            'class_id' => 1,
            ]);
        }
    You can add multiple records and use loops or other logic to insert more data.

4. Run the Seeder:

    To execute the seeder and insert the data into your database, run the following command:

        php artisan db:seed --class=StudentSeeder

    This command will execute the run() method of the StudentSeeder class and populate the database with the defined data.

You can create multiple seeders for different tables or specific data sets. By running the seeders, you can easily populate your database with initial or test data, making it convenient for development or testing purposes.