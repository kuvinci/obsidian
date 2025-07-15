#PHP #Laravel #routing #redirects 
`web.php` → Роути для внутрішніх сторінок продукту

`api.php` → Роути для білду API’х (Наприклад `Route::middleware('auth:sanctum')`)

```php
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::delete($uri, $callback);
Route::options($uri, $callback);

Route::match(['get', 'post'], '/', function () {
    //
});
 
Route::any('/', function () {
    //
});
```

## ****[Dependency Injection](https://laravel.com/docs/9.x/routing#dependency-injection)****

Можно тайп хінтить в роутах, `service container` розбереться з ін’єкціями сам

```php
use Illuminate\\Http\\Request;
 
Route::get('/users', function (Request $request) {
    // ...
});
```

## ****[Redirect Routes](https://laravel.com/docs/9.x/routing#redirect-routes)****

```php
Route::redirect('/here', '/there'); // Regular redirect with 302 status
Route::redirect('/here', '/there', 301); // Custom status
Route::permanentRedirect('/here', '/there'); // Permanent redirect (301 status)
```

## ****[View Routes](https://laravel.com/docs/9.x/routing#view-routes)****

```php
Route::view('/welcome', 'welcome'); // УРЛ, шлях до вью файла
Route::view('/welcome', 'welcome', ['name' => 'Taylor']); // Третій аргумент це дані, які треба передати до вью
```

## ****[The Route List](https://laravel.com/docs/9.x/routing#the-route-list) - Список консольних команд для роутів**

## **[Route Parameters](https://laravel.com/docs/9.x/routing#route-parameters)**

```php
Route::get('/user/{id}', function ($id) {
    return 'User '.$id;
});
```

## Named Routes

Можно навісити “ярличок” на роут і потім використовувати роут по ярличку

```php
Route::get('/user/profile', 'UserProfileController@show')->name('profile.show'); // За допомогою name() дали назву роуту

$url = route('profile.show'); // <http://yourapp.com/user/profile>
```

Ще можно генерувати роути одразу з параметром

```php
Route::get('/user/{id}', 'UserController@show')->name('user.show');

$url = route('user.show', ['id' => 1]); // <http://yourapp.com/user/1>
```

Ще з ними легше робити редіректи (не треба слати на хардкодед урл)