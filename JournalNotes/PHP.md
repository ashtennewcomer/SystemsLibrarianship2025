# Log Entry

**March 05, 2025**

Today, I installed and configured PHP on my virtual machine. 

PHP is a **server-side** programming language and must be installed on your server.

1. Updated my virtual machine:
  * `sudo apt update`
  * `sudo apt -y upgrade`
  * `sudo apt -y autoremove`
  * `sudo apt clean`
2. Installed program:
  * `sudo apt install php libapache2-mod-php`
3. Restarted apache2:
  * `sudo systemctl restart apache2`
4. Confirmed installed version
  * `php -v`
5. Checked apache2 status:
  * `systemctl status apache2`
  * Looked for `active` `loaded` and `enabled`
6. Checked install:
  * `cd /var/www/html/`
  * `sudo nano info.php`
7. Added the following code to the file:
  * ```
    <?php
    phpinfo();
    ?>
    ```
8. Checked the file using my IP address:
  * `http://34.29.236.71/info/php`
9. Removed the file:
  * `sudo rm /var/www/html/info.php`
10. Configured apache2 by duplicating the `dir.conf` file and editing the original file:
  * `cd /etc/apache2/mods-enabled/`
  * `sudo cp dir.conf dir.conf.bak`
  * `sudo nano dir.conf`
11. Changed the order of the code in the file:
  * `DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm`
12. Checked apache2 configuration:
  * `apachectl configtest`
  * Received `Syntax Ok` message
13. Restarted apache2:
  * `sudo systemctl reload apache2`
  * `sudo systemctl restart apache2`
  * `systemctl status apache2`
14. Created an `index.php` file:
  * `cd /var/www/html/`
  * `sudo nano index.php`
15. Added HTML and PHP using code from textbook to act as a simple browser detector
16. Checked my public IP address again
  * It was still displaying the original `index.html` file
  * Realized I had mistyped `index.php` in the `dir.conf` file
  * Fixed this mistake and restarted apache2
  * Site is now correctly showing the `index.php` file; states that my browser is Google Chrome and my os is Windows.
