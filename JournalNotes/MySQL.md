# Log Entry

**March 08, 2025**

Today, I installed and configured MySQL on my virtual machine.

MySQL is a relational database management system and I configured it to work with the Apache web server and the PHP programming language from previous weeks.

1. Updated my virtual machine:
  * `sudo apt update`
  * `sudo apt -y upgrade`
  * `sudo apt -y autoremove`
  * `sudo apt clean`
2. Installed MySQL:
  * `sudo apt install mysql-server`
3. Checked status:
  * `systemctl status mysql`
4. Ran a post installation script:
  * `sudo mysql_secure_installation`
  * Selected `yes` and `0` when prompted
5. Logged into the database as root user:
  * `sudo mysql -u root`
6. Created/set up regular user account:
  * `sudo mysql -u root`
  * `create user 'opacuser'@'localhost' identified by 'XXXXXXXXXX';`
    * I replaced the `XXXXXXXXX` with my password
  * I received the prompt `Query Ok`
7. Created a practice database:
  * `create database opacdb default character set utf8mb4 collate utf8mb4_unicode_ci;`
8. Granted access to `opacuser`
  * `grant all privileges on opacdb.* to 'opacuser'@'localhost' with grant option;`
9. Exited as root user
10. Edited `.bashrac` file:
  * `nano .bashrc`
  * Added `export MYSQL_PS1="[\d]> "` to the bottom of the file
  * Saved and exited the file
  * Sourced the file using `source ~/.bashrc`
11. Logged in as regular user:
  * `mysql -u opacuser -p`
  * The `-p` at the end prompts it to ask for my password
12. Switched to `opacdb` database:
  * `use opacdb;`
13. Created and defined new table:
  * ```create table books (
        id int unsigned not null auto_increment,
        author varchar(150) not null,
        title varchar(150) not null,
        copyright year(4) not null,
        primary key (ID)
);```
14. Added records into the table:
  * ```insert into books (author, title, copyright) values
('Jennifer Egan', 'The Candy House', '2022'),
('Imbolo Mbue', 'How Beautiful We Were', '2021'),
('Lydia Millet', 'A Children\'s Bible', '2020'),
('Julia Phillips', 'Disappearing Earth', '2019');```
  * I messed this part up and accidentally duplicated a line when I was trying to use the up arrow to use a previous command. I knew I could delete the line but I didn't like that the ID numbers would be messed up. I ended up googling how to delete the entire table using `DROP` and redid this section.
15. Tested commands using the supplied commands in the textbook (not going to type all of that out again)
  * Some of these commands altered the table by adding a publisher field; I then added the publisher information for each book
  * I also deleted one of the books by author and added two more entries
16. Installed PHP support for MySQL:
  * `sudo apt install php-mysql php-mysqli`
17. Restarted Apache2 and MySQL:
  * `sudo systemctl restart apache2`
  * `sudo systemctl restart mysql`
18. Created `login.php` file in document root's parent directory and changed the group ownership and permissions:
  * ```cd /var/www
sudo touch login.php
sudo chmod 640 login.php
sudo chown :www-data login.php
ls -l login.php
sudo nano login.php```
19. Added content to the file using `nano`:
  *```<?php // login.php
$db_hostname = "localhost";
$db_database = "opacdb";
$db_username = "opacuser";
$db_password = "XXXXXXXXX";
?>
```
20. Created a file titled `opac.php` in `/var/www/html`:
  * `cd /var/www/html`
  * `sudo nano opac.php`
21. Copied code from textbook into the `opac.php` file and saved
22. Tested syntax:
  * `sudo php -f /var/www/login.php`
  * sudo php -f /var/www/html/opac.php`
22. Tested the site by visiting `http://34.29.236.71/opac.php`
  * Site was functional and correct

MySQL Commands:
  * Always add a `;` at the end of MySQL commands
  * `show databases;` to list all databases
  * Use `\q` to exit MySQL server prompt
  * `describe XXXXXX;` to view table
  * `select * from books;` to view all records
  * `DELETE` will delete rows from a table
  * `DROP` will delete an entire database

Notes:
  * I learned that I automatically type a `u` everytime I type `q` which was very frustrating when I first began using these commands
  * Need to figure out if there is a way to cancel a command without running it in case of typos
  
