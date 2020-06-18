# Reverse Proxy  

* Client의 요청을 받아서, 이를 Upstream 서버에 넘겨주고 그것이 처리한 응답을 받아서 다시 Client에 넘겨준다.  

## 1. proxy_pass directive 사용  

* **마지막에 / 를 붙여주자**
```
server {

  location /php/ {
    proxy_pass 'http://127.0.0.1:8001/';
  }
  
  location /goserver/ {
    proxy_pass 'http://127.0.0.1:8002/'
  }

}
```
* / 의 여부에 따라서 URI가 바뀐다.  
```
http://mydomain.com/php/api/ping
---> 변환
  http://127.0.0.1:8002/api/ping
```
<br/><br/>

* location 마지막에 / 가 없는 경우
```
  location /php {
    proxy_pass 'http://127.0.0.1:8001/';
  }
```
다음의 path를 upstream 서버가 받게 된다.  
```
//ping 
```
<br/><br/>

* proxy_pass 마지막에 / 가 없는 경우
```
  location /php {
    proxy_pass 'http://127.0.0.1:8001';
  }
```
다음의 path를 upstream 서버가 받게 된다.  
```
/php/ping
```


## 2. NginX에서 Header 추가  

#### 2.1. add_header  
* nginx에서 **클라이언트**로 응답보낼 때 추가되는 헤더  

```
location /php/ {
  add_header hello world    # Key Value 
  proxy_pass 'http://localhost:8002/'
}
```
* 응답 결과
```
curl -i http://localhost/goserv/ping    

HTTP/1.1 200 OK
Server: nginx/1.14.0 (Ubuntu)
Date: Thu, 18 Jun 2020 06:44:59 GMT
Content-Type: application/json; charset=utf-8
Content-Length: 15
Connection: keep-alive
hello: world      <<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<

{"ok":"가나"}%  
```

#### 2.2. proxy_set_header  
* nginx에서 **서버**로 보낼 때 추가되는 헤더  
```
location /php/ {
  proxy_set_header hello world    # Key Value 
  proxy_pass 'http://localhost:8002/'
}
```



