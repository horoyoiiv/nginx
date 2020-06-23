
# Cache-Control  
* static 자원들에 대한 cache-control  

```
        location ~* \.(css|js|jpg|png)$ {
            access_log off;
            add_header Cache-Control public;
            add_header Pragma public;
            add_header Vary Accept-Encoding;
            expires 1m;
        }


```

# gzip  
* 압축된 response 보내기  
* gzip을 통해서 압축한 후 **응답**을 보낸다.  
* `Accept
![스크린샷, 2020-06-23 15-02-34](https://user-images.githubusercontent.com/62331555/85366581-9cc80c80-b562-11ea-9fef-f90c911466c0.png)  


## 2. gzip 사용  

```

http {
   
    include mime.types;
     
    gzip on;  # child context will override it.  
    gzip_comp_level 3;
    gzip_types text/css text/javascript; # array directives


```
* 사용 전  
```
Size 1.3 K
Time 4   ms
```

<br/><br/>
* **Contents-Encoding : gzip** 이라고 응답 헤더에 온다.  
* 사용 후  
```
Size 885 B
Time 70  ms
```
