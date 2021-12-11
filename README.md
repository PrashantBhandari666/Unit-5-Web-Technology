# Introduction to Advance Server Side Issue

## Database Connectivity:
------------------------

With PHP, you can connect to and manipulate databases.

MySQL is the most popular database system used with PHP.

* MySQL is a database system used on the web
* MySQL is a database system that runs on a server
* MySQL is ideal for both small and large applications
* MySQL is very fast, reliable, and easy to use
* MySQL uses standard SQL
* MySQL compiles on a number of platforms
* MySQL is free to download and use
* MySQL is developed, distributed, and supported by Oracle Corporation
* MySQL is named after co-founder Monty Widenius's daughter: My


### **Creating Connection**
In PHP you can easily do this using the ``mysqli_connect()`` function. All communication between PHP and the MySQL database server takes place through this connection. Here're the basic syntaxes for connecting to MySQL using MySQLi and PDO extensions:

Syntax: MySQLi, Procedural way
```PHP
$conn = mysqli_connect("hostname", "username", "password", "database");
```

Syntax: MySQLi, Object Oriented way
```PHP
$conn = new mysqli("hostname", "username", "password", "database");
```

Syntax: PHP Data Objects (PDO) way
```PHP
$conn = new PDO("mysql:host=hostname;dbname=database", "username", "password"); 
```

### **Close the Connection**

The connection will be closed automatically when the script ends. To close the connection before, use the following:

```PHP
mysqli_close($conn); 
```

**Example:**
```PHP
<?php
$servername = "localhost";
$database = "mmc";
$username = "root";
$password = "";
// Create connection
$conn = mysqli_connect($servername, $username, $password, $database);
// Check connection
if (!$conn) 
{
    die("Connection failed: " . mysqli_connect_error());
}
echo "Connected successfully";
mysqli_close($conn);
?>
```

## Creating an SQL statement 
----------------------------

### ``INSERT``

The ``INSERT INTO`` statement is used to add new records to a MySQL table:

Syntax:
```SQL
INSERT INTO table_name (column1, column2,...) VALUES (value1, value3,...);
```

Example:
```SQL
INSERT INTO student (StudentID, FirstName, LastName, RollNo, City) VALUES (1, 'Prashant', 'Bhandari', 39, 'Birtamode');
INSERT INTO student VALUES (4, 'Ram', 'Dahal', 67, 'Chandragadi');
```
Data can be entered into MySQL tables by executing SQL ``INSERT`` statement through PHP function ``mysql_query()``.

Example program:
```PHP
<?php
$servername = "localhost";
$database = "mmc";
$username = "root";
$password = "";
// Create connection
$conn = mysqli_connect($servername, $username, $password, $database);
// Check connection
if (!$conn) 
{
    die("Connection failed: " . mysqli_connect_error());
}
// Attempt insert query execution
$sql = "INSERT INTO student VALUES (4, 'Ram', 'Dahal', 67, 'Chandragadi');";
if(mysqli_query($conn, $sql))
{
    echo "Records inserted successfully.";
} 
else
{
    echo "ERROR: Could not able to execute $sql. " . mysqli_error($conn);
}
mysqli_close($conn);
?>
```

### ``SELECT``

The ``SELECT`` statement is used to select data from one or more tables:

Syntax:
```SQL
SELECT column_name(s) FROM table_name
```

or we can use the ``*`` character to select ALL columns from a table:

```SQL
SELECT * FROM table_name 
```

Example Program:
```PHP
<?php
$servername = "localhost";
$database = "mmc";
$username = "root";
$password = "";
// Create connection
$conn = mysqli_connect($servername, $username, $password, $database);
// Check connection
if (!$conn) 
{
    die("Connection failed: " . mysqli_connect_error());
}
// Attempt select query execution
$sql = "SELECT * FROM student";
$result = mysqli_query($conn, $sql);

if (mysqli_num_rows($result) > 0) {
  // output data of each row
  while($row = mysqli_fetch_assoc($result))
  {
    echo "Id =". $row['StudentID']. " Name =". $row['FirstName']. $row['LastName'] ." Rollno = ".$row['RollNo']. " City=" .$row['City'];
    echo "<br>";
  }
} 
else 
{
  echo "0 results";
}
mysqli_close($conn);
?>
```
the function ``mysqli_num_rows()`` checks if there are more than zero rows returned.

If there are more than zero rows returned, the function ``mysqli_fetch_assoc()`` puts all the results into an associative array that we can loop through. The ``while()`` loop loops through the result set and outputs the data.

### ``UPDATE``

The ``UPDATE`` statement is used to update existing records in a table:

Syntax:
```SQL
UPDATE table_name SET column1=value1, column2=value2,... WHERE some_column=some_value  
```

```SQL
UPDATE student SET FirstName="Yugesh" WHERE StudentID=2;
```

Example Program:

```PHP
<?php
$servername = "localhost";
$database = "mmc";
$username = "root";
$password = "";
// Create connection
$conn = mysqli_connect($servername, $username, $password, $database);
// Check connection
if (!$conn) 
{
    die("Connection failed: " . mysqli_connect_error());
}
// Attempt update query execution
$sql = "UPDATE student SET FirstName='Ram Bhadadur' WHERE StudentID=2;";
if(mysqli_query($conn, $sql))
{
    echo "Records updated successfully.";
} else
{
    echo "ERROR: Could not able to execute $sql. " . mysqli_error($conn);
}
mysqli_close($conn);
?>
```

### ``DELETE``

The ``DELETE`` statement is used to delete records from a table:

Syntax:
```SQL
DELETE FROM table_name WHERE some_column = some_value 
```

Example:
```SQL
DELETE FROM student WHERE StudentID=3;
```

Example Program:

```PHP
<?php
$servername = "localhost";
$database = "mmc";
$username = "root";
$password = "";
// Create connection
$conn = mysqli_connect($servername, $username, $password, $database);
// Check connection
if (!$conn) 
{
    die("Connection failed: " . mysqli_connect_error());
}
// Attempt delete query execution
$sql = "DELETE FROM student WHERE StudentID=3;";
if(mysqli_query($conn, $sql))
{
    echo "Records deleted successfully.";
} else
{
    echo "ERROR: Could not able to execute $sql. " . mysqli_error($conn);
}
mysqli_close($conn);
?>
```
## Authentication:
-------------------
Authentication is the process of verifying the identity of user or information. User authentication is the process of verifying the identity of user when that user logs into a computer system.

The main objective of authentication is to allow authorized users to access the computer and to deny access to the unauthorized users.

### Anonymous Access:

An anonymous access is a process that allows a user to acess to a website anonymously.

### Authentication by IP address

IP address authentication is the traditional method of identifying users requesting access to vendor databases. Users gain access based on their computer or site IP address (numerical address), eliminating the need for user IDs and passwords.

Suppose you want to allow the website to the IP addresses in the range of ``123.121.0.1`` to ``123.121.0.255``. In the given example, we have defined an array of the allowed IP addresses that can view the page for this, we have taken three array elements. The array``("123", "121", "0")`` limits the users who can view the page to the users with an IP address in the range of ``123.121.0.1`` to ``123.121.0.255``. The current user's IP address is taken by using a global variable ``'$_SERVER'`` and stored in a variable ``'$REMOTE_ADDR'``.

```PHP
<?php
	$allowed_ip = array("123", "121", "0");
	$REMOTE_ADDR = $_SERVER["REMOTE_ADDR"];
	$remote_ip = explode(".", $REMOTE_ADDR);
	$permitted = 1;
	for($i = 0; $i < sizeof($allowed_ip); $i++) 
    {
		if($remote_ip[$i] != $allowed_ip[$i])
        {
			$permitted = 0;
		}
	}
	if($permitted == 1) 
    {
		echo 'Welcome, You are authorized to access this page.';
	}
	else
    {
		echo 'Access Denied';
	}
?>
```
>replace the ``$allowed_ip`` array values with your allowed IP address. If you want to restrict the page to only one IP address, then pass all the four values of IP address as four elements in ``$allowed_ip`` array.

### Integrated Window Authentication

Integrated Windows Authentication (IWA) refers to a set of authentication protocols, NTLM, Kerberos, and SPNEGO, that are used to provide transport-level security. You can configure IBM® Integration Bus to provide an IWA-secured service on an integration node running on any operating system, and to consume an IWA-secured service on an integration node running on Windows, when you are using the HTTP, SOAP, and REST nodes.

IWA provides authentication to users who have an identity in Windows domains or in the Kerberos Key Distribution Center (KDC). IWA includes the protocols NT Lan Manager (NTLM), Kerberos, and Simple and Protected Negotiation (SPNEGO)

## Cookies
-------------
A cookie is often used to identify a user. A cookie is a small file that the server embeds on the user's computer. Each time the same computer requests a page with a browser, it will send the cookie too. With PHP, you can both create and retrieve cookie values.

### **Cookies With PHP**

A cookie is created with the ``setcookie()`` function.

Syntax:

```PHP
setcookie(name, value, expire, path, domain, secure, httponly);
```
>Only the ``name`` parameter is required. All other parameters are optional.

**PHP Create/Retrieve a Cookie**

The following example creates a cookie named ``"user"`` with the value ``"Prashant Bhandari"``. The cookie will expire after 30 days (86400 * 30). The ``"/"`` means that the cookie is available in entire website (otherwise, select the directory you prefer).

We then retrieve the value of the cookie ``"user"`` (using the global variable ``$_COOKIE``). We also use the ``isset()`` function to find out if the cookie is set:

```PHP
<?php
$cookie_name = "user";
$cookie_value = "Prashant Bhandari";
setcookie($cookie_name, $cookie_value, time() + (86400 * 30), "/"); // 86400 = 1 day
?>
<html>
    <body>
    <?php
    if(!isset($_COOKIE[$cookie_name]))
    {
        echo "Cookie named '" . $cookie_name . "' is not set!";
    } 
    else 
    {
        echo "Cookie '" . $cookie_name . "' is set!<br>";
        echo "Value is: " . $_COOKIE[$cookie_name];
    }
    ?>
    </body>
</html> 
```
>**Note:** The ``setcookie()`` function must appear BEFORE the ``<html>`` tag.

>**Note:** The value of the cookie is automatically URLencoded when sending the cookie, and automatically decoded when received (to prevent URLencoding, use ``setrawcookie()`` instead).

**Modify a Cookie Value**

To modify a cookie, just set (again) the cookie using the ``setcookie()`` function:

Example:
```PHP
<?php
$cookie_name = "user";
$cookie_value = "Sachin Khadka";
setcookie($cookie_name, $cookie_value, time() + (86400 * 30), "/"); // 86400 = 1 day
?>
<html>
    <body>
    <?php
    if(!isset($_COOKIE[$cookie_name]))
    {
        echo "Cookie named '" . $cookie_name . "' is not set!";
    } 
    else 
    {
        echo "Cookie '" . $cookie_name . "' is set!<br>";
        echo "Value is: " . $_COOKIE[$cookie_name];
    }
    ?>
    </body>
</html> 
```

**Delete a Cookie**

To delete a cookie, use the ``setcookie()`` function with an expiration date in the past:

```PHP
<?php
// set the expiration date to one hour ago
setcookie("user", "", time() - 3600);
?>
<html>
    <body>
    <?php
    echo "Cookie 'user' is deleted.";
    ?>
    </body>
</html> 
```

**Check if Cookies are Enabled**

The following example creates a small script that checks whether cookies are enabled. First, try to create a test cookie with the ``setcookie()`` function, then count the ``$_COOKIE`` array variable:

```PHP
<?php
setcookie("test_cookie", "test", time() + 3600, '/');
?>
<html>
    <body>
    <?php
    if(count($_COOKIE) > 0) 
    {
        echo "Cookies are enabled.";
    } 
    else
    {
        echo "Cookies are disabled.";
    }
    ?>
    </body>
</html> 
```

## File Handeling in PHP
----------------------

File handling is needed for any application. For some tasks to be done file needs to be processed. File handling in PHP is similar as file handling is done by using any programming language like C. PHP has many functions to work with normal files. Those functions are:

### ``fopen()`` 

PHP ``fopen()`` function is used to open a file. First parameter of ``fopen()`` contains name of the file which is to be opened and second parameter tells about mode in which file needs to be opened, e.g.,

```PHP
<?php
$file = fopen(“file.txt”,'w');
?>
```
Files can be opened in any of the following modes :

* ``w`` – Opens a file for write only. If file not exist then new file is created and if file already exists then contents of file is erased.
* ``r`` – File is opened for read only.
* ``a`` – File is opened for write only. File pointer points to end of file. Existing data in file is preserved.
* ``w+`` – Opens file for read and write. If file not exist then new file is created and if file already exists then contents of file is erased.
* ``r+`` – File is opened for read/write.
* ``a+`` – File is opened for write/read. File pointer points to end of file. Existing data in file is preserved. If file is not there then new file is created.
* ``x`` – New file is created for write only.

### ``fread()``

After file is opened using ``fopen()`` the contents of data are read using ``fread()``. It takes two arguments. One is ``file pointer`` and another is ``file size`` in bytes, e.g.,

```PHP
<?php
$filename = "file.txt";
$file = fopen( $filename, 'r' );
$size = filesize( $filename );
$filedata = fread( $file, $size );
?>
```

### ``fwrite()``

New file can be created or text can be appended to an existing file using ``fwrite()`` function. Arguments for ``fwrite()`` function are ``file pointer`` and ``text`` that is to written to file. It can contain optional third argument where ``length of text`` to written is specified, e.g.,

```PHP
<?php
$filename = "file.txt";
$file = fopen( $filename, 'w');
$text = "I am Prashant Bhandari\n";
fwrite($file, $text);
?>
```

### ``fclose()``

file is closed using ``fclose()`` function. Its argument is file which needs to be closed, e.g.,

```PHP
<?php
$file = fopen("file.txt", 'r');
//some code to be executed
fclose($file);
?>
```

## PHP Form Handling
---------------------
The PHP superglobals ``$_GET`` and ``$_POST`` are used to collect form-data.`

Example
```PHP
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>form</title>
</head>
<body>
    <form action="#" method="post">
    Name: 
    <input type="text" name="name"><br>
    E-mail: 
    <input type="text" name="email"><br>
    <input type="submit" name="btn">
    </form>
    <?php
    if(isset($_POST["btn"]))
    {
       $name=$_POST["name"];
       $email=$_POST["email"];
       echo "Welcome $name <br>" ;
       echo "Your Email is $email" ;
    }
    ?>
</body>
</html>
```

### GET vs. POST

Both GET and POST create an array (e.g. array( key1 => value1, key2 => value2, key3 => value3, ...)). This array holds key/value pairs, where keys are the names of the form controls and values are the input data from the user.

Both GET and POST are treated as ``$_GET`` and ``$_POST``. These are superglobals, which means that they are always accessible, regardless of scope - and you can access them from any function, class or file without having to do anything special.

$_GET is an array of variables passed to the current script via the URL parameters.

$_POST is an array of variables passed to the current script via the HTTP POST method.

### When to use GET?

Information sent from a form with the GET method is visible to everyone (all variable names and values are displayed in the URL). GET also has limits on the amount of information to send. The limitation is about 2000 characters. However, because the variables are displayed in the URL, it is possible to bookmark the page. This can be useful in some cases.

GET may be used for sending non-sensitive data.

>Note: GET should NEVER be used for sending passwords or other sensitive information!

### When to use POST?

Information sent from a form with the POST method is invisible to others (all names/values are embedded within the body of the HTTP request) and has no limits on the amount of information to send.

Moreover POST supports advanced functionality such as support for multi-part binary input while uploading files to server.

However, because the variables are not displayed in the URL, it is not possible to bookmark the page.

>Developers prefer POST for sending form data.
