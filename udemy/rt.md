

# Return 와 Rewrite  

## 1. Return  

* `location` 문맥 안에서 **return 307**을 사용하면 **Redirect** 응답을 보낸다.  
```
return 307 URI
```

#### 1.1. 예제  
<br/><br/>
```
    server {
        
        listen 8888;
        server_name 127.0.0.1;
        
        root /sites/demo;

        location = /logo {
            return 307 /thumb.png;
        }
        
    }
```
```
www.mydomain.com/logo

위의 요청을 보내면 location 헤더에 재요청 보낼 URI가 오고 아래의 요청을 브라우져에서 다시 보냄.

www.mydomain.com/thumb.png
```


## 2. Rewrite  
* NginX 내에서 다시 URI을 바꿔서 처리한다.  
```
rewrite urlA urlB
```
* urlA로 들어온 요청을 urlB로 변환하여 다시 설정에서 match 패턴을 찾는다.  

```
    server {
    
        root /sites/demo;

        rewrite ^/user/(\w+) /greet/$1;   $1 은 캡쳐된 (\w+)을 의미한다.
        
        location /greet/jane {
            return 200 "Hello jane";
        }
        
   }     
```

```
www.domain.com/user/jane
으로 들어온 요청은 

/greet/jane 으로 바뀌게 되어

location /greet/jane 으로 들어가게 된다.
```





