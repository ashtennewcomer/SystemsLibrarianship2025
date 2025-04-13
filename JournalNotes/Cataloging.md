# Log Entry

**April 13, 2025**

In week 11, I created a cataloging module for my website. This was a very simplified cataloging fucntion that allowed me to enter new book records into my database. Real-world cataloging modules would contain much more information and would include features like MARC to format the authority and bibliographic records and content to make it more graphically attractive such as images and formatting. 

1. Updated VM.
2. Changed to HTML directory: `cd /var/www/html`
3. Created cataloging directory: `sudo mkdir cataloging`
4. Changed to cataloging directory: `cd cataloging`
5. Created index file: `sudo nano index.html`
6. Added code to index file:
``` 
<!DOCTYPE html>
<html>
<head>
    <title>Enter Records</title>
</head>
<body>
    <h1>OPAC Library Administration</h1>

    <p>This is the library administration page for entering records into the OPAC.</p>
    <p>Please do not use this page unless you are an authorized cataloger.</p>

    <form action="insert.php" method="post">
        <label for="author">Author:</label>
        <input type="text" name="author" id="author" required><br><br>

        <label for="title">Book Title:</label>
        <input type="text" name="title" id="title" required><br><br>

        <label for="publisher">Publisher:</label>
        <input type="text" name="publisher" id="publisher" required><br><br>

        <label for="copyright">Copyright:</label>
        <input type="number" name="copyright" id="copyright" min="1000" max="2300" required>

        <input type="submit" value="Submit">
    </form>
</body>
</html>
```

This code creates a form for users to enter bibliographic data. A PHP script is still required in order for this form to communicate and add the data into our MySQL database and `books` table.


7. Created PHP insert script: `nano insert.php`
8. Added code to insert file:
```
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cataloging: Data Entry</title>
</head>
<body>

<h1>Cataloging: Data Entry</h1>

<?php

// Load MySQL credentials
require_once '/var/www/login.php';

// Enable MySQL error reporting
mysqli_report(MYSQLI_REPORT_ERROR | MYSQLI_REPORT_STRICT);

// Establish connection
$conn = new mysqli($db_hostname, $db_username, $db_password, $db_database);
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// Prepare and bind SQL statement
$stmt = $conn->prepare("INSERT INTO books (author, title, publisher, copyright) VALUES (?, ?, ?, ?)");
$stmt->bind_param("ssss", $author, $title, $publisher, $copyright);

// Set parameters and execute statement
$author = $_POST["author"];
$title = $_POST["title"];
$publisher = $_POST["publisher"];
$copyright = $_POST["copyright"];

if ($stmt->execute() === TRUE) {
    echo "New record created successfully";
} else {
    echo "Error: " . $stmt->error;
}

// Close statement and connection
$stmt->close();
$conn->close();
?>

<p><a href='index.html'>Return to Cataloging Page</a></p>
<p><a href='../mylibrary.html'>Return to Library Home Page</a></p>
</body>
</html>
```

This code requires MySQL credentials to be entered and establishes a connection. A prepared statement is created to use data entered on the web form and formats it to be entered into the database table.

In order to keep the database secure, I used an authentification code provided by Apache2 called `htpasswd`. In order to use this, I created an authentification file on my Apache2 directory.

7. Created authentification file: `sudo htpasswd -c /etc/apache2/.htpasswd libcat`
8. Edited Apache2 configuration module to control access: `sudo nano /etc/apache2/apache2.conf`
  * In line 172, changed `None` to `All`:
  ```
  <Directory /var/www/>
  Options Indexes FollowSymLinks
  AllowOverride All
  Require all granted
</Directory>
  ```
9. Changed to cataloging directory: `cd /var/www/html/cataloging`
10. Created file: `sudo nano .htaccess`
11. Added to file:
  ``` 
  AuthType Basic
AuthName "Authorization Required"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
  ```
12. Checked that the configuration file is okay: `apachectl configtest`
13. Restarted Apache2 and check status:
  * `sudo systemctl restart apache2`
  * `systemctl status apache2`
14. Changed group ownership of `/var/www/html` to `www-data`
  * `sudo chown :www-data /var/www/html`
  * `sudo chmod -R g+s /var/www/html`
15. Visited cataloging website and log in: `http://34.29.236.71/cataloging/`
16. Addeded book records: 
  * `Sunrise on the Reaping by Suzanne Collins (Scholastic Press, 2025)`
  * `Magnolia Parks by Jessa Hastings (House of Hastings, 2021)`
17. Successfully searched for newly added records

