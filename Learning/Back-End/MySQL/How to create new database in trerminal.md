#back-end #mysql #database

#### Якщо при `sudo mysqld_safe --skip-grant-tables &` викидає помилку:
```
sudo mkdir -p /var/run/mysqld
```
```
sudo chown mysql:mysql /var/run/mysqld
```
Далі:
```
sudo systemctl stop mysql
sudo mysqld_safe --skip-grant-tables &
mysql -u root
FLUSH PRIVILEGES;
```
Тут пароль !def
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY '![def]';
```
```
EXIT;
```

Reboot PC
```
mysql -u root -p

CREATE DATABASE [database_name];

GRANT ALL PRIVILEGES ON [database_name].* TO 'root'@'localhost';
```