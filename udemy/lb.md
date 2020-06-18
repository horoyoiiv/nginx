# Load Balancer  

## 1. upstream directive  
서버를 **그룹화**화여 설정하는 context  

```
upstream php_serves {
  server localhost:8001;
  server localhost:8002;
  server localhost:8003;
}
```
<br/><br/>

## 2. LB 해보기  

```
http {
   
    include mime.types;
     
    upstream php_servers {
        server localhost:8001;
        server localhost:8002;
        server localhost:8003;
    }

    server {
        
        listen 8888;
        server_name 127.0.0.1;
        
        root /sites/demo;
        
        location /php/ {
            proxy_pass http://php_servers/;       # proxy_pass directive를 통해 usptream 서버 그룹을 넘겨준다.
        }
         
    }
}
```

## 3. Load Balancer Option  


#### 3.1. ip_hash  
* **ip_hash** or **sticky session**  
```
    upstream php_servers {
        ip_hash;
        server localhost:8001;
        server localhost:8002;
        server localhost:8003;
    }
```

<br/><br/>
#### 3.2. least_conn    
* connection이 가장 적은 server로 포워딩하지만, weight도 고려한다.  
```
    upstream php_servers {
        least_conn;
        server localhost:8001;
        server localhost:8002;
        server localhost:8003;
    }
```












