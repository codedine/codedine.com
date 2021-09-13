---
title: Laravel Repository Pattern using Interface
path: /laravel-repository-pattern-using-interface
date: 2021-09-12
summary: Laravel Repository Pattern using interface is the best way of maintaining your big projects. It can be used in any programming language.
tags: ['repository pattern', 'laravel', 'interface']
categories: ['Laravel', 'PHP']
thumbnail: ./2021-09-12-laravel-repository-pattern.png
---

## Introduction
Laravel Repository Pattern using interface is the best way of maintaining your big projects. If you understand principle behind repository pattern you can use it in any frameworks or programming languages as a best practice. Okay fine lets start.

## Laravel Repository Pattern
Repository pattern is a kind of container where you store your business logic. Let's say you're developing a product and selling in the market and then you're providing a service for the product. So each customer wants different changes in the products then how you could manage them all? Here the repository pattern helps you can have separate container of business logic (repositories pattern) for the each customers this won't affect your products core functionalities.

## Repository Pattern Using Interface
Enough theories lets start digging laravel repository pattern using interface. In this tutorial we going to create **Post Controller** which contains CURD operation for a post. We are going to create a Repository which implements an Interface and we're going to register the repository and interface using [Laravel IoC.](https://laravel.com/docs/container) First [install Laravel and Setup a database connection](https://codedine.com/install-laravel-6/) and then we will create routes, model, migrations and seeds for the Post.

## Model, Seeds and Migrations
Create a Post model with migration as well as controller with following artisan command

```bash
php artisan make:model Post -mc
```

Here **\-mc** creates migration as well as controller for the Post model. In post table migration let add some fields

```php
public function up()
{
    Schema::create('posts', function (Blueprint $table) {
        $table->bigIncrements('id');
        $table->string('title');
        $table->string('slug')->unique();
        $table->longText('data');
        $table->timestamps();
    });
}
```

Add factory for posts table using following command. Factories used to create fake records for testing.

```bash
php artisan make:factory PostFactory
```

Inside `PostFactory`

```php
<?php

/* @var $factory \Illuminate\Database\Eloquent\Factory */

use Faker\Generator as Faker;
use Illuminate\\Support\\Str;

$factory->define(\App\Models\Post::class, function (Faker $faker) {

    $title = $faker->sentence($nbWords = 6, $variableNbWords = true);

    return [
        'title' => $title,
        'slug'  => Str::slug($title),
        'data'  => $faker->paragraph($nbSentences = 8, $variableNbSentences = true)
    ];

});
```

Now add the factory to the DatabaseSeeder and run the migration command along with seeds to populate some records. `database/seeds/DatabaseSeeder.php` add following line inside run method

```bash
factory(App\Models\Post::class, 20)->create();
```

and Run

```bash
php artisan migrate:fresh --seed
```

## Post Controller and its Routes
Add Post Controller by artisan command

```bash
php artisan make:controller PostController
```

Now create routes for the post controller

```php
<?php

// routes/web.php

Route::get('posts/find-by', [App\Http\Controllers\PostController::class, 'findBy'])->name('post.findBy');
Route::resource('posts', App\Http\Controllers\PostController::class)->except(['create', 'edit']);
```

## Post Interface and Post Repository

Now we need to create an Interface for Post. An Interface is nothing but the skeleton for the repository if all methods inside the interface are not available on repository it throws an error. so interfaces are useful when it comes to big applications. I usually create Interface inside `app/Contracts`

```php
<?php
// app/Contracts/PostInterface

namespace App\Contracts;

interface PostInterface
{
    public function index();

    public function find($post);

    public function findBy($att, $column);

    public function store($request);

    public function update($post, $request);

    public function destroy($post);
}
```

Let's create a PostRepository which implements PostInterface with logic for CURD operations. I usually create Repository namespaces in app/Repositories directory

```php
<?php

namespace App\Repositories;

use App\Contracts\PostInterface;
use App\Models\Post;

class PostRepository implements PostInterface 
{
    protected $post;

    public function __construct(Post $post)
    {
        $this->post = $post;
    }

    public function index()
    {
        return $this->post->all();
    }

    public function find($post)
    {
        return $this->post->findOrFail($post);
    }

    public function findBy($att, $column)
    {
        return $this->post->where($att, $column)->get();
    }

    public function store($request)
    {
        return $this->post->create($request);
    }

    public function update($post, $request)
    {
        $post = $this->post->findOrFail($post);
        $post->update($request->all());
        return $post;
    }

    public function destroy($post)
    {
        return $this->post->findOrFail($post)->delete();
    }
}
```

## Register Interface and Repository in Service Provider

Create a Service Provider let say PostServiceProvider

php artisan make:provider PostServiceProvider

Now register Post Interface and Repositories in Post Service Provider inside register method

```php
public function register()
{    
    $this->app->bind('App\Contracts\PostInterface', 'App\Repositories\PostRepository');
}
```

In `config/app.php` register the service provider we have created inside providers array add.

`App\Providers\PostServiceProvider::class`

Finally, in Post Controller constructor lets call Post Repository.

```php
<?php

namespace App\Http\Controllers;

use App\Repositories\PostRepository;

class PostController extends Controller
{
    protected $post;

    public function __construct(PostRepository $post)
    {
        $this->post = $post;
    }

    public function index()
    {
        return $this->post->index();
    }

    public function store()
    {
        return $this->post->store(request()->all());
    }

    public function show($post)
    {
        return $this->post->find($post);
    }

    public function findBy()
    {
        return $this->post->findBy('slug', request('slug'));
    }

    public function update($post)
    {
        return $this->post->update($post, request()->all());
    }

    public function destroy($post)
    {
        return $this->post->destroy($post);
    }
}
```


That's it, take a look what we have done we have implemented **Interface** and injected to the **PostController**. 

## Conclusion
Thanks to Laravel IoC container to made this easier and possible on PHP. 
Thanks for reading :) any queries? use comment section below.