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
