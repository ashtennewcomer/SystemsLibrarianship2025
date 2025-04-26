# Log Entry

**April 26, 2025**

Koha is an open source ILS that includes features such as circulation, cataloging, an OPAC, patron accounts, etc. 
My Koha site will be linked on my library's website under multiple click links inlcuding "Log In", "Items Out", "Borrowing History", "Holds", "Catalog", and "Browse Books".

This week I installed and configured Koha with my new virtual machine.

1. Set up new gcloud virtual machine (for increased RAM):
  * Series: E2
  * Machine Type: 2 vCPU
  * Memory: 4 GB
  * Disk size: 20 GB
  * Networking: Allow HTTP traffic
  * Network tags: `koha-8080`
  * Operating system: Ubuntu 22.04
2. Set up Google Cloud firewall:
  * VPN Network -> Firewall
  * Create a firewall rule
  * Name: `koha-opac`
  * Description: `Open port 8080 for the OPAC`
  * Targets: Specified target tags
  * Target tags: `koha-8080`
  * Source IPv4 ranges: `0.0.0.0/0`
  * Specified protocols and ports: 
    * TCP
    * Ports: 8080
  * Create
3. Updated and upgraded local repositories and servers
4. Autoremoved and cleaned
5. Installed `gnupg2` and `apt-transport-https`: `sudo apt install gnupg2 apt-transport-https`
6. Rebooted
7. Logged in as root user
8. Added Koha repository to our server: `echo 'deb http://debian.koha-community.org/koha stable main' | sudo tee /etc/apt/sources.list.d/koha.list`
9. Downloaded GPG key: `wget -qO- https://debian.koha-community.org/koha/gpg.asc | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/koha.gpg > /dev/null`
10. Inspected key: `gpg --show-keys /etc/apt/trusted.gpg.d/koha.gpg`
11. Installed Koha:
  * Synced new repository with Koha remote repository: `apt update`
  * Viewed packaged information for Koha: `apt show koha-common`
  * Installed software: `apt install koha-common`
12. Created backup of the default configuration file
  ``` 
  cd /etc/koha/
  cp koha-sites.conf koha-sites.conf.backup
  ```
13. Installed nano: `sudo apt install nano`
14. Opened config file in nano: `nano /etc/koha/koha-sites.conf`
15. In nano file, changed `INTRAPORT="80"` to `INTRAPORT="8080"`
16. Installed mysql-server `apt install mysql-server`
17. Set MySQL root password: `mysqladmin -u root password XXXXXXXX`
18. Enabled URL rewriting and CGI functionality:
  ```
  a2enmod rewrite
  a2enmod cgi 
  ```
19. Resrted Apache2: `systemctl restart apache2`
20. Created a database for Koha: `koha-create --create-db bibliolib`
21. Configured Apache2 to listen on port 8080:
  * `nano /etc/apache2/ports.conf`
  * Under the `Listen 80` line, added `Listen 8080`
22. Tested Apache2 config changes: `apachectl configtest`
23. Restarted Apace2: `systemctl restart apache2`
24. Disabled the default Apache2 setup: `a2dissite 000-default`
25. Enabled traffic compression using `deflate`: `a2enmod deflate`
26. Enabled the bibliolib site: `a2ensite bibliolib`
27. Reloaded Apache2's configs: `systemctl reload apache2`
28. Restarted Apache2: systemctl `restart apache2`
29. Retrieved Koha username and password from `nano /etc/koha/sites/bibliolib/koha-conf.xml`
  * config stanza: line 252
  * user: line 257
  * password: line 258
30. Retrieved IP address for new vm and visited: `http://34.59.169.237:8080`
31. Finished setting up Koha through web installer
  * During this process, I received an error code; restarted the web installed from the beginning and it worked fine

Once I was logged into Koha, I:
* Set up my admin account
* Configured the OPAC:
  * More -> Administration -> System Preferences -> OPAC
  * `OPACBaseURL`: `http://34.59.169.237`
* Set up and deleted sample patron account
* Set up and deleted sample libraries
* Imported bib records for a few books including:
  * Fourth Wing
  * Educated
  * A Little Life
  * Circe
  * The Systems Librarian
  * The Systems Librarian Guide to Computers
* Checked out books to patron
* Placed items on hold for patron
* Configured settings for what patrons can view from their account
* Deleted patron circulation history
