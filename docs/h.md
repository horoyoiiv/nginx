

# header  

* nginx 에서는 유저에게 응답하기 전 **헤더**를 추가할 수 있다.  
* **add_header** 디렉티브 : K - V 를 지정할 수 있다.  

```
http {
    
    # virtual host 1
    server {
        listen 80;
        server_name naver.com;


        location / {
            add_header my_header "Great Day";   
            add_header Cache-Control public;
            expires 1m;

            root /var/www/html;  
        }       
        
        ....
```


* 응답 헤더에는 다음과 같은 `Cache-Control` 헤더가 추가된다.  
```
Cache-Control: max-age=600
Cache-Control: public
```

