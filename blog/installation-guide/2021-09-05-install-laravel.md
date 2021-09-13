---
title: How to install Laravel 8? PHP Framework
path: /install-laravel-8-php-framework
date: 2021-09-05
summary: So what is Laravel and how to install Laravel 8.0? Laravel is the super cool framework for PHP created by Taylor Otwell.
tags: ['installation guide', 'laravel', 'install laravel']
categories: ['Laravel', 'Installation Guide', 'PHP']
thumbnail: ./2021-09-05-install-laravel.png
---

## Introduction

So what is Laravel and how to install Laravel 8.0? Laravel is the super cool framework for PHP created by Taylor Otwell. 
Laravel is known for its scalability and flexibility, it uses MVC architecture pattern and more you can read more about it in [laravel official page](https://laravel.com). 
In this post I'm going to install Laravel 8.0 which is the current stable version. It is always the best practice to use current stable version because you will get a good support from Laravel community. 
You can even use Long Term Supported version (Larvel 8.0 LTS) when your application is bigger and it need a support for longer term. 
Let us assume you've already installed PHP and let get started.

## Install Composer

Before we start install laravel we need Composer which is dependency package manager for php. Laravel uses composer to manage its dependencies. You can download and install composer from its [official site](https://getcomposer.org/download/) and select your corresponding PHP version.

## Install Laravel 8.0

Before we install Laravel 8.0 you need to check your server meets following requirements. Alternatively you can use Laravel Homestead which includes all the packages and requirements for the Laravel development. I will create a another post on installing Laravel Homestead.

*   PHP >= 7.3.0
*   OpenSSL PHP Extension
*   PDO PHP Extension
*   Mbstring PHP Extension
*   Tokenizer PHP Extension
*   XML PHP Extension
*   Ctype PHP Extension
*   JSON PHP Extension
*   BCMath PHP Extension

## Via Laravel Installer

First, download the Laravel installer using Composer:

composer global require laravel/installer

Once installed, the `laravel new` command will create a fresh Laravel installation in the directory you specify. For instance, `laravel new blog` will create a directory named `blog`

laravel new blog

## or Via Composer

Alternatively, you can also install Laravel by using the Composer `create-project` command in your terminal.

```bash
composer create-project --prefer-dist laravel/laravel blog
```

if you want to install specific version of Laravel you can use the following command. Let say I want to install Laravel 5.5

composer create-project laravel/laravel blog 5.5.\*

that's it Laravel now installed successfully.

## Run Laravel

If you've installed laravel locally you can use following `artisan serve` command to run laravel in development server [http://localhost:8000](http://localhost:8000)

php artisan serve

## Database Configuration (MySQL)

Let us assume you've install mysql and created a database name `blog`. Now setup the database configuration inside the **.env** file.

```bash
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=blog
DB_USERNAME=root
DB_PASSWORD=root
```

Thanks for reading :) Any queries leave comments.