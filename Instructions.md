Dependencies::
sudo apt-get installmbsting
sudo apt-get install php7.1-xml
sudo apt-get install php5.6-mysql/php7.2-mysql
On dev site change CACHE_DRIVER from file => array
Cloning project - Permisions:
	sudo chmod -R 777 laravel_blog/storage
	sudo chmod 755 -R laravel_blog
	chmod -R o+w laravel_blog/storage
	chown -R sergio:sergio laravel_blog/
	php artisan cache:clear
	
php.ini -> extension = pdo_mysql (uncomment)

Virtual server:

Hosts:
blog.testing.local

Serving:
php artisan serve --port=8080
	And if you want to run it on port 80, you probably need to sudo:
		sudo php artisan serve --port=80
Kill: 
	ps -aux | grep artisan
		kill 'PID NUMBER'

Errors:
Failed to clear cache. Make sure you have the appropriate permissions
	the "data" directory (storage/framework/cache/data) doesn't exist you	 	will have this error.
	This "data" folder doesn't exist by default on a fresh/new installation.
	Creating the "data" directory at (storage/framework/cache) manually 		should fix this issue.
one must pay careful attention to the insecure permissions of user’s public_html folders. The following commands will look in every user’s html folder and make the appropriate CHMOD to allow php to properly execute under SUPHP. Don’t forget to also check for files owned by ‘nobody’ or ‘root’ — they will also fail with a 500 error.
	find /home/*/public_html/ -type d -print0 | xargs -0 chmod 0755 # For directories
	find /home/*/public_html/ -type f -not -name "*.pl" -not -name "*.cgi" -not -name "*.sh" -print0 | xargs -0 chmod 0644 # For files
	find /home/*/public_html/ -type f -name "*.cgi" -print0 -o -name "*.pl" -print0 -o -name "*.sh" -print0 | xargs -0 chmod 0755 # For CGI/Scripts
	http://djlab.com/2009/06/cpanel-suphp-chmod-all-files-644-and-all-folders-755/

Your database driver is missing. To solve the probelm
	For ubuntu: For mysql database.
	sudo apt-get install php5.6-mysql/php7.2-mysql



Yes, Laravel file and database drivers doesn't support tags. What you can do to while developing is change the driver to array in your .env file.
	CACHE_DRIVER=array 

PDO_MYSQL - not supported => https://forum.matomo.org/t/you-need-to-enable-the-pdo-and-pdo-mysql-extensions-in-your-php-ini-file/261
