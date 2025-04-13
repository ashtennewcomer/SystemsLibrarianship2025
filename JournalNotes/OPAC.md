# Log Entry
**April 13, 2025**

In week 10, I created a simple OPAC for my website. This was a very simplified version of an OPAC while an integrated library system would be much more complex. 

This OPAC works on the very basic concept of entering data into a database and then retrieving said data. A real ILS would use other technologies such as HTML or JavaScript to present the data in a more user-friendly way. ILSes would also contain more features such as filters/refiners, circulation information, authority records, etc.

In a prior module, I created a MySQL database called `opacdb` which contains a table called `books`. During this week, I used a PHP code to allow us to search the `books` table.

1. Update VM
2. Change to HTML directory: `cd /var/www/html`
3. Create HTML page: `sudo nano mylibrary.html`
4. Enter the following code into `mylibrary.html`
  ``` <!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>MySQL Server Example</title>
    </head>
<body>

    <h1>A Basic OPAC</h1>

    <p>In the form below, <b>optionally</b> enter text in the search field.
    Your search query will search by author, title, or publisher.
    Capitalization is not necessary.
    It's okay to enter partial information, like part of an author's, title's, or publisher's name.</p>

    <p>You can leave the search field empty and only enter dates.
    Regardless, both start and end dates are required for all searches.
    You can use the date fields to limit results, too.
    I added some extra records, which you can view to know what you can query:</p>

    <p><a href="opac.php">OPAC</a></p>

    <p>This is very much a toy, stripped down
    <a href="https://en.wikipedia.org/wiki/Online_public_access_catalog">OPAC</a>.
    The records are basic.
    Not only do they not conform to <a href="https://www.loc.gov/marc/">MARC</a>,
    they don't even conform to something as simple as <a href="https://www.dublincore.org/">Dublin Core</a>.

    <p>I also don't provide options to select different fields, like author, title, or publisher fields.
    Instead the search field below searches all the fields (author, title, publisher) in our <b>books</b> table.</p>

    <p>The key idea is to get a sense of how an OPAC works, though.</p>

    <h2>My Basic Library OPAC</h2>

    <form method="post" action="search.php">
        <label for="search">Search Terms (optional):</label>
        <input type="text" name="search" id="search">
        
        <br>
        
        <label for="start_date">Start Date:</label>
        <input type="date" name="start_date" id="start_date" required>
        
        <br>
        
        <label for="end_date">End Date:</label>
        <input type="date" name="end_date" id="end_date" required>
        
        <br>
        
        <input type="submit" value="Search">
    </form>

</body>
</html>
```
5. Create PHP script: `sudo nano search.php`
6. Enter the following code into `search.php`:
   ``` <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Search Results</title>
<style>
    table {
        border-collapse: collapse;
        width: 100%;
    }
    th, td {
        border: 1px solid black;
        padding: 8px;
        text-align: left;
    }
</style>
</head>
<body>

    <h1>Search Results</h1>

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

    if ($_SERVER["REQUEST_METHOD"] == "POST") {
        $search = trim($_POST['search']);
        $start_date = $_POST['start_date'];
        $end_date = $_POST['end_date'];

        // Prepared statement to prevent SQL injection
        $stmt = $conn->prepare("SELECT * FROM books 
                                WHERE (author LIKE ? OR title LIKE ? OR publisher LIKE ?) 
                                AND copyright BETWEEN ? AND ?");

        // Use wildcard search
        $search_param = "%$search%";
        $stmt->bind_param("sssss", $search_param, $search_param, $search_param, $start_date, $end_date);
        $stmt->execute();
        $result = $stmt->get_result();

        if ($result->num_rows > 0) {
            echo "<table>";
            echo "<tr><th>ID</th><th>Author</th><th>Title</th><th>Publisher</th><th>Copyright</th></tr>";

            while ($row = $result->fetch_assoc()) {
                echo "<tr>";
                echo "<td>" . htmlspecialchars($row["id"]) . "</td>";
                echo "<td>" . htmlspecialchars($row["author"]) . "</td>";
                echo "<td>" . htmlspecialchars($row["title"]) . "</td>";
                echo "<td>" . htmlspecialchars($row["publisher"]) . "</td>";
                echo "<td>" . htmlspecialchars($row["copyright"]) . "</td>";
                echo "</tr>";
            }

            echo "</table>";
        } else {
            echo "<p>No results found.</p>";
        }

        $stmt->close();
    }

    $conn->close();
    ?>

    <p><a href="mylibrary.html">Return to search page</a></p>

</body>
</html>
```
This code establishes the connection between the website and MySQL. The code includes a prepared statement to search the database and inputs the variables that the user enters on the website. If the executed command returns results, the code tells it how to display the results.

7. Test the website to make sure the OPAC is functioning: `http://34.29.236.71/mylibrary.html`
8. Modify `books` table:
  * Log in as `opacuser`: `mysql -u opacuser -p`
  * ``` insert into books
(author, title, publisher, copyright) values
('Emma Donoghue', 'Room', 'Little, Brown \& Company', '2010'),
('Zadie Smith', 'White Teeth', 'Hamish Hamilton', '2000');
```
