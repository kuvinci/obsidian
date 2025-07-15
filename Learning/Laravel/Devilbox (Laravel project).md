#devilbox 
Based on this tutorial - https://devilbox.readthedocs.io/en/latest/examples/setup-laravel.html

1. `cd devilbox`
2. `docker stop $(docker ps -a -q)` Kill all containers
3. `docker-compose up -d`
4. `docker-compose exec php bash`
5. `mkdir [project-name]`
6. `cd [project-name]`
7. `laravel new [laravel-project-name]`
8. `ln -s [project-name]/public/ htdocs` Create htdocs (Devilbox required)
9. `chmod -R 777 [laravel-project-name]/storage/` Permissions for storage
10. `chmod -R 777 [laravel-project-name]/bootstrap/cache/` Permissions for cache
	1. OR `chmod -R 777 [laravel-project-name]` for all project directories
11. Edit `hosts` file with new domain (Domain name here - https://localhost/vhosts.php)