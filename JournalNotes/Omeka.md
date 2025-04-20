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

**April 20, 2025**

Today I played around with the actual Omeka site and its appearance. I was able to change the theme and add a few different pictures under a title called "My Favorite Books". I know this is not a typical collection type that would be displayed in a digital library, but I just wanted to try adding a few items to a collection. I did not add any metadata other than title and creator, but I do have previous experience with this type of work.

1. Download the theme "Minimalist" from the Omeka website.
2. Upload this to my VM using the browser interface.
3. Navigate to the root directory using `sudo su`
4. Move "minimalist" zip file from my root directory into my Omeka themes directory: `sudo mv theme-minimalist-v2.5.4.zip /var/www/html/digitallibrary/themes/theme-minimalist-v2.5.4.zip`
5. Exit root directory
6. Navigate to themes folder: `cd /var/www/html/digitallibrary/themes`
7. Unzip "minimalist" theme folder: `sudo unzip theme-minimalist-v2.5.4.zip`
8. Delete zip folder: `sudo rm theme-minimalist-v2.5.4.zip`
9. Exit VM
10. Go back to the Omeka admin site at `http://34.29.236.71/digitallibrary/admin`
11. Log in and navigate to the appearance tab
12. Select "Minimalist" theme
13. Configure settings to include my library's logo and a short description.
14. Added a collection titled "My Favorite Books"
15. Added 6 items to the collection that included the book cover, title, and author
