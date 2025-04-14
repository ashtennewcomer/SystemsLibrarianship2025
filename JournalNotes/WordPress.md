# Log Entry

**April 13, 2025**

WordPress is an open source is a free, open source content management system that is widely used for blogs and building websites. Many libraries use WordPress for their main websites and supplement with other services such as ILSes. 

This week, I installed and configured WordPress with my virtual machine. 

1. Check my system to see if it meets the WP requirements:
  * `php --version`
  * `mysql --version`
2. Updated my virtual machine
3. Added additional PHP modules: `sudo apt install php-curl php-xml php-imagick php-mbstring php-zip php-intl`
4. Restarted Apache2 and MySQL:
  * `sudo systemctl restart apache2`
  * `sudo systemctl restart mysql`
5. Changed to HTML directory: `cd /var/www/html`
6. Downloaded the latest version of WordPress: `sudo wget https://wordpress.org/latest.zip`
7. Installed unzip program: `sudo apt install zip`
8. Unzipped WP file: `sudo unzip latest.zip`
9. Switched to root user: `sudo su`
10. Logged in to MySQL as root user: `mysql -u root`
11. Created new user and password (replaced XXXXXXXXX:) `create user 'wordpress'@'localhost' identified by 'XXXXXXXXX';` 
12. Created new database: `create database wordpress;`
13. Granted privileges: `grant all privileges on wordpress.* to 'wordpress'@'localhost';`
14. Examined output and exited: `show databases;`
15. Changed to wordpress directory: `cd /var/www/html/wordpress`
16. Copied and renamed wp config file: `sudo cp wp-config-sample.php wp-config.php`
17. Edited wp config file:`sudo nano wp-config.php`
18. Disabled FTP uploads by adding `define('FS_METHOD','direct');` to the end of the config file
19. Renamed wp directory to change URL: `sudo mv /var/www/html/wordpress /var/www/html/nwcrlibrary`
20. Changed file ownership: `sudo chown -R www-data:www-data /var/www/html/nwcrlibrary`
  * Had trouble with this until I realized that I had changed my directory name and needed to reflect that in the command
21. Ran install script: `http://http://34.29.236.71/nwcrlibrary/wp-admin/install.php`
22. Created a username and password through the browser interface
23. Found a template to use for my website; ended up using the `Books Library` theme
24. Customized my webpage with a logo I created, changed some of the headers, added pictures, added fake contact information, etc.
  * This was by far the most difficult part of the assignment. I do not find WordPress to be very beginner user friendly and had to use some breathing techniques while trying to edit my layout. 
