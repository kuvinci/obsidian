#PHP #Laravel #views #blade

## Views
```php
// View stored in resources/views/greeting.blade.php
<html>
    <body>
        <h1>Hello, {{ $name }}</h1>
    </body>
</html>
```

##### From a route:
```php
Route::get('/', function () {
    return view('welcome'); // Виведе welcome.blade.php
});
```

##### From controller:
```php
public function show($id)
{
    return view('user.profile', ['user' => User::findOrFail($id)]);
}
```
*Перший аргумент - `resources/views/user.profile.blade.php`*
*Другий аргумент - `[user => user_data_from_DataBase]`*

## Blade
- `@if`, `@elseif`, `@else`, `@endif` - for conditional statements
- `@foreach`, `@endforeach` - for looping over arrays
- `@isset`, `@endisset` - to determine if a variable is set
- `@empty`, `@endempty` - to determine if a variable is empty

##### Conditional Statements:
```php
@if (count($records) === 1)
    There is one record!
@elseif (count($records) > 1)
    There are multiple records!
@else
    There are no records!
@endif
```

##### Loops:
```php
@foreach ($users as $user)
    <p>This is user {{ $user->id }}</p>
@endforeach

// It's like an if(){} inside a foreach(){}
@forelse ($users as $user)
    <li>{{ $user->name }}</li>
@empty
    <p>No users</p>
@endforelse
```

##### Include other Blade files:
```php
@include('header')

<div>
    <!-- Content of your web page -->
</div>

@include('footer')
```

##### Layouts:
*Define master layout*
```php
// Stored in resources/views/layouts/app.blade.php

<html>
    <head>
        <title>App Name - @yield('title')</title>
    </head>
    <body>
        @section('sidebar')
            This is the master sidebar.
        @show

        <div class="container">
            @yield('content')
        </div>
    </body>
</html>
```

*Then extend that layout in child views*
```php
// Stored in resources/views/home.blade.php

@extends('layouts.app')

@section('title', 'Page Title')

@section('sidebar')
    @parent

    <p>This is appended to the master sidebar.</p>
@endsection

@section('content')
    <p>This is my body content.</p>
@endsection
```

##### @yield and @section
`@yield`  - it's like a placeholder in the template

For example here is a **base view**
```php
// Stored in resources/views/layouts/app.blade.php
<html>
    <head>
        <title>App Name - @yield('title')</title>
    </head>
    <body>
        <div class="container">
            @yield('content')
        </div>
    </body>
</html>
```

Then in **child view** that extends our **base view** we specify both title and content with `@section`:
```php
// Stored in resources/views/home.blade.php
@extends('layouts.app')

@section('title', 'Home Page')

@section('content')
    <p>This is my body content for the Home Page.</p>
@endsection
```

It looks like this:
- Parent view with `@yield(title)` that marks a place for child to put title there with @section
	- Child view with `@section('Hello World')` renders a Hello World title instead of @yield placeholder

##### @parent
`@parent` - will append instead of rewriting a section content

For example:
*Base view*
```php
// Stored in resources/views/layouts/app.blade.php
<html>
    <head>
        <!-- ... -->
    </head>
    <body>
        @section('scripts')
            <script src="app.js"></script>
        @show
    </body>
</html>
```

*Child view that **appends** new script file to **@section('scripts')***
```php
// Stored in resources/views/home.blade.php
@extends('layouts.app')

@section('scripts')
    @parent
    <script src="home.js"></script>
@endsection
```