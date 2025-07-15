#Laravel #controllers 
### Create Controller:
`php artisan make:controller UserController`

### Basic Controller:
```php
<?php

namespace App\\Http\\Controllers;

use Illuminate\\Http\\Request;

class UserController extends Controller
{
    /**
     * Show the profile for the given user.
     *31
     * @param  int  $id
     * @return Response
     */
    public function show($id)
    {
        return view('user.profile', ['user' => User::findOrFail($id)]);
    }
}
```

Метод show приймає $id, отримує з бази даних користувача і віддає дані.

### Controller Routing:
```php
Route::get('/user/{id}', 'UserController@show');
```

### You can create a Resource Controllers with:
`php artisan make:controller UserController --resource`

```php
Route::resource('users', 'UserController');
```

The **`Route::resource`** method will generate all necessary routes for the **`index`**, **`create`**, **`store`**, **`show`**, **`edit`**, **`update`**, and **`destroy`** actions.