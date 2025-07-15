DB_CONNECTION=mysql  
DB_HOST=db  
DB_PORT=3306  
DB_DATABASE=eddy_db  
DB_USERNAME=eddy_user  
DB_PASSWORD=eddy_password  
  
DB_CONNECTION_LEGACY=mysql_legacy  
DB_HOST_LEGACY=db3  
DB_PORT_LEGACY=3306  
DB_DATABASE_LEGACY=eddy_db3  
DB_USERNAME_LEGACY=eddy_user3  
DB_PASSWORD_LEGACY=eddy_password3

config/database.php
```
'mysql' => [  
'driver' => 'mysql',  
'host' => env('DB_HOST', '127.0.0.1'),  
'port' => env('DB_PORT', '3306'),  
'database' => env('DB_DATABASE', 'forge'),  
'username' => env('DB_USERNAME', 'forge'),  
'password' => env('DB_PASSWORD', ''),  
'unix_socket' => env('DB_SOCKET', ''),  
'charset' => 'utf8mb4',  
'collation' => 'utf8mb4_unicode_ci',  
'prefix' => '',  
'prefix_indexes' => true,  
'strict' => true,  
'engine' => null,  
'options' => extension_loaded('pdo_mysql') ? array_filter([  
PDO::_MYSQL_ATTR_SSL_CA_ => env('MYSQL_ATTR_SSL_CA'),  
]) : [],  
],  
  
'mysql_legacy' => [  
'driver' => 'mysql',  
'host' => env('DB_HOST_LEGACY', '127.0.0.1'),  
'port' => env('DB_PORT_LEGACY', '3308'),  
'database' => env('DB_DATABASE_LEGACY', 'forge'),  
'username' => env('DB_USERNAME_LEGACY', 'forge'),  
'password' => env('DB_PASSWORD_LEGACY', ''),  
'unix_socket' => env('DB_SOCKET_LEGACY', ''),  
'charset' => 'utf8mb4',  
'collation' => 'utf8mb4_unicode_ci',  
'prefix' => '',  
'strict' => true,  
'engine' => null,  
],
```