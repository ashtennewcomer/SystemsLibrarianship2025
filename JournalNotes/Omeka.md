# Log Entry

**April 19, 2025**

Omeka is an "open-source web publishing platforms for sharing digital collections and creating media-rich online exhibits." 
My Omeka site will be linked on my library's site under the "Digital Library" tab.

This week I installed and configured Omeka with my virtual machine.

1. Updated my virtual machine.
2. Checked my system to see if it meets the Omeka requirements:
3. Installed ImageMagick `sudo apt install imagemagicl`
4. Enabled Apache mod_rewrite `sudo a2enmod rewrite`
5. Restarted Apache
6. Created new user and database in MySQL:
  ```
  sudo su
  mysql -u root
  create user 'omeka'@'localhost" identified by 'XXXXXXXXXXXX';
  create database omeka;
  grant all privileges on omeka.* to 'omeka'@'localhost';
  show database'
  \q
  ```
7. Changed to `/var/www/html` directory
8. Downloaded latest version of Omeka Classic
  ```
  sudo wget https://github.com/omeka/Omeka/releases/download/v3.1.2/omeka-3.1.2.zip
  sudo unzip latest.zip
  ```
  * During this part of the process, I had issues with unzipping the file. It seemed like it was working but I think I somehow interrupted the process. When I tried to run it again, it asked me something about writing over a WordPress file. I went back and deleted `omeka-3.1.2.zip`.
9. Downloaded Omeka again and then ran `sudo unzip omeka-3.1.2` which worked correctly
10. Changed directory to 'omeka' using `sudo mv omeka-3.1.2 omeka`
11. Edited `db.ini` file using `nano db.ini`:
  ```
  host = "localhost"
  username = "omeka"
  password = "XXXXXXXXXXXX"
  dbname = "omeka"
  ```
12. This did not let me save the file so I then ran the same command but used `sudo nano db.ini` which worked
13. Changed user and owner of omeka directory `sudo chown -R www-data:www-data /var/www/html/omeka
14. Checked ownership in `/var/www/html` and `/var/www/html/omeka` using `ll` command
15. Restarted Apache and MySQL using `sudo systemctl restart` command
16. Completed setup in web browser which was successful
17. Linked Omeka on my WordPress site using the `DIGITAL LIBRARY` tab
18. Decided to go back and change the name to "digitallibrary" using `sudo mv /var/www/html/omeka /var/www/html/digitallibrary`
19. Updated hyperlink on my WordPress site to reflect the change
