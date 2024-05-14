<p align="center">
  <a href="https://github.com/i-rin-eam">
    <img src="https://avatars.githubusercontent.com/u/154800878?s=400&u=5d18880cc28646190a19a971bfcdbc54644eab07&v=4" alt="Logo" width="100" height="100">
  </a> 
<h1 align='center'>Rretrieve Image from MySql database</h1>
<h3 align='center'>
    <a href="https://www.youtube.com/watch?v=CzOvRGdiO-0">Watch the video</a> to learn how to retrieve image from MySql database in Android Studio using PHP and Volley.
</p>
  
## Step 1: Request Runtime Storage Permissions: <a href="https://www.youtube.com/watch?v=I3nGvV--2IU">Watch the video</a>
  
## Step 2: Upload Image into MySQL Database: <a href="https://youtu.be/CzOvRGdiO-0?si=6OAEjsnn9BdT8rj8">Watch the video</a>

## Step 3: Here is `get.php` code: 
```php
<?php

// Database configuration settings
$hostName = "localhost"; 
$userName = "database_username"; 
$password = "database_password"; 
$dbName = "database_name"; 

// Establish connection with the MySQL database
$conn = mysqli_connect($hostName, $userName, $password, $dbName);

// Check if the database connection was successful
if (!$conn) {
    // If connection failed, terminate script execution and display an error message
    die("Connection failed: " . mysqli_connect_error());
}

// Set the character set of the database connection to 'utf8mb4' for full Unicode support
mysqli_set_charset($conn, "utf8mb4");

// Base URL for where images are stored
$baseUrl = "https://example.com/images/";

// Initialize an array to hold the data that will be output
$data = array();  

// SQL query to retrieve all data from the usersData table
$getQuery = "SELECT * FROM image_table";  
$response = mysqli_query($conn, $getQuery);  

foreach ($response as $item) {
    // Extract each row's data
    $id = $item['id'];  
    $name = $item['name'];  
    $image = $item['image'];  

    // Prepare user information to be JSON encoded
    $userInfo['id'] = $id;  
    $userInfo['name'] = $name;  
    $userInfo['images'] = $baseUrl . $image;  // Concatenate base URL with the image file name
    array_push($data, $userInfo);  
} 

// Set the header to output JSON with UTF-8 encoding
header('Content-Type: application/json; charset=utf-8');

// Encode data array to JSON and output it
echo json_encode($data, JSON_UNESCAPED_UNICODE);

// Close the database connection
mysqli_close($conn);

?>
```
## Step 4: Here is `JSONArray Request` code: 
```java
    RequestQueue queue = Volley.newRequestQueue(MainActivity.this);
        JsonArrayRequest jsonArrayRequest = new JsonArrayRequest(Request.Method.GET, url, null, new Response.Listener<JSONArray>() {
            @Override
            public void onResponse(JSONArray response) {
            
            }
        }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
                Toast.makeText(MainActivity.this, "Fail to get the data..", Toast.LENGTH_SHORT).show();
            }
        });
        queue.add(jsonArrayRequest);
```
## Authors

**MD YEAMIN** - Android Software Developer <a href="https://www.youtube.com/@LearnWithYeamin">**(Learn With Yeamin)**</a> 

<h1 align="center">Thank You ❤️</h1>
