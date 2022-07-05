# Digitalocean-Database-Cluster-with-laravel-5
Connection between digital ocean database cluster and laravel 5


1. Create database cluster in digitalocean 

	https://docs.digitalocean.com/products/databases/mysql/how-to/create/

2. Creating a new MySQL User and Database in our server

	-> mysql -u MYSQL_USER -p -h MYSQL_HOST -P MYSQL_PORT

	-> CREATE DATABASE bnfexpress;

	-> CREATE USER bnfexpress-user'@'%' IDENTIFIED WITH mysql_native_password BY 'MYSQL_PASSWORD';

	-> GRANT ALL ON bnfexpress.* TO bnfexpress-user'@'%';

3. Add new database cluster setting in laravel 
	
	a. In .env file

		DB_CONNECTION=mysql
		DB_HOST=127.0.0.1 
		DB_PORT=3306 
		DB_DATABASE=database1 
		DB_USERNAME=root 
		DB_PASSWORD=secret 

		DB_CONNECTION_SECOND=mysql 
		DB_HOST_SECOND=testing-database-do-user-9898878-0.b.db.ondigitalocean.com
		DB_PORT_SECOND=28465 
		DB_DATABASE_SECOND=bnfexpress 
		DB_USERNAME_SECOND=bnfexpress-user
		DB_PASSWORD_SECOND=secret

	b. In config/database.php

	 	'mysql' => [
		    'driver'    => env('DB_CONNECTION'),
		    'host'      => env('DB_HOST'),
		    'port'      => env('DB_PORT'),
		    'database'  => env('DB_DATABASE'),
		    'username'  => env('DB_USERNAME'),
		    'password'  => env('DB_PASSWORD'),
		],

		'mysql2' => [
		    'driver'    => env('DB_CONNECTION_SECOND'),
		    'host'      => env('DB_HOST_SECOND'),
		    'port'      => env('DB_PORT_SECOND'),
		    'database'  => env('DB_DATABASE_SECOND'),
		    'username'  => env('DB_USERNAME_SECOND'),
		    'password'  => env('DB_PASSWORD_SECOND'),
		],

	c. Schema
		To specify which connection to use, simply run the connection() method

			Schema::connection('mysql2')->create('some_table', function($table)
			{
			    $table->increments('id'):
			});

	d. Query Builder

		$users = DB::connection('mysql2')->select(...);

	e. Eloquent

		Set the $connection variable in your model

		class SomeModel extends Eloquent {
		    protected $connection = 'mysql2';
		}


REFERENCE

https://www.digitalocean.com/community/tutorials/how-to-set-up-a-scalable-laravel-6-application-using-managed-databases-and-object-storage#step-2-creating-a-new-mysql-user-and-database

https://codelapan.com/post/how-to-use-multiple-database-connections-in-laravel-8

https://laravel.com/docs/5.2/database

https://stackoverflow.com/questions/31847054/how-to-use-multiple-databases-in-laravel

