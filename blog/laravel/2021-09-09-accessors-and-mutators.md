---
title: Laravel Accessors Mutators (Getters and Setters)
path: /laravel-accessors-mutators-example
date: 2021-09-09
summary: Prettier is nothing but a code formatter, which re-formats the code. In this article we are going to see using prettier in laravel.
tags: ['accessors', 'mutators', 'accessors and mutators', 'getters and setters']
categories: ['Laravel', 'PHP']
thumbnail: ./accessors-and-mutators/accessors-and-mutators.png
---

## Introduction - Laravel Mutators Accessors

[`Eloquent Mutators`](https://laravel.com/docs/5.8/eloquent-mutators) are used to modify the value of the particular field in the database before we save or update the object model. Whereas `Accessors` will format the value from database and returns in the format we want to. let see both in action. In Laravel in `users` table we have following fields:

1.  first_name
2.  last_name
3.  email
4.  password
5.  created_at
6.  updated_at

## Mutators in Action

In the above field when everytime we save or update the User model password field needed to be `bcrypt`. So to avoid writing the bcrypt function again and again we need to set mutators for password field in User model. Inside the User model lets create a function called `setPasswordAttribute`when we create a mutator function we need to keep in mind that mutator function should have following syntax

```bash
set<fieldName>Attribute($value)
```

where `$value`is the field value we pass. Following function is the mutator for password field, everytime use create or update the User model with password field it will automatically bcrypts the password and save to the database.

```php
public function setPasswordAttribute($value)
{
    $this->attributes['password'] = bcrypt($value);
}
```

## Accessors in Action

In users table we have two fields that is `first_name` and `last_name` when we want to display full name of users we will write as `{{ first_name }} {{ last_name }}` in blade template. But this method is inappropriate when we use restfull api's each time we need append, to avoid this we use accessors. Accessors function should have following syntax.

```bash
get<fieldName>Attribute()
```

Note that filedName must be in upper camel case.

```php
function getFullNameAttribute()
{
    return $this->attributes['first_name'] . ' ' . $this->attributes['last_name'];
}
```

Here full name is not in the users table we need to append it to the Users model as follows.

```php
protected $appends = ['full_name'];
```

## Full Example Code
Now our User model will return with full_name attribute, And finally full example of our User model will be as follows.

```php
<?php

namespace App;

use Illuminate\Notifications\Notifiable;
use Illuminate\Contracts\Auth\MustVerifyEmail;
use Illuminate\Foundation\Auth\User as Authenticatable;

class User extends Authenticatable
{
    use Notifiable;

    protected $fillable = [
        'first_name', 'last_name', 'email', 'password',
    ];

    protected $hidden = [
        'password', 'remember_token',
    ];
	
    protected $appends = ['full_name'];

    public function setPasswordAttribute($value) 
    { 
        $this->attributes['password'] = bcrypt($value); 
    }
	
    function getFullNameAttribute() 	
    { 
         return $this->attributes['first_name'] . ' ' . $this->attributes['last_name']; 
    }
}
```

The above Model which has function `setPasswordAttribute` will save the password with bcrypted value (which is basically called Setters or Mutators),
And the function `getFullNameAttribute` will append first name and last name retrived from database (which is called Getters or Accessors)

## Conclusion
So basically mutators will modify (mutates) the data sent from the request, while accessors will return the data that are modified during the request. 

That's it any suggestions or queries drop in comment box below or you can [contact us](/contact-us/).