

# reverse proxy  

* `리버스 프록시`로서의 nginx  
* **리버스 프록시** : WAS 혹윽 WAS로 구성된 클러스터 앞단에 배치되어, 클라이언트의 요청을 대신 받아 이를 `upstream 서버` 포워딩하는 서버.  

#### [nginx 공식 문서](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)  

## 1. 도입  

* 뒷단의 upstream 서버에 HTTP 혹은 그외 프로토콜로 요청을 `전달`할 수 있다.  

## 2. proxy_pass  
* `location` directive 에서 사용되며, 뒷단의 서버 주소를 입력한다.  
* `도메인 네임` 혹은 `IP 주소`를 기입한다.  

```
location /auth {
  proxy_pass http://127.0.0.1:8007;
}
```
* /auth/ path로 들어오는 모든 요청은 proxy_pass 주소의 서버로 **포워딩**된다.  

```
1. http://127.0.0.1:80/auth 입력

2. nginx가 받은 후 proxy_pass

3. http://127.0.0.1:8007/auth <- location을 붙여서 포워딩
```

## 3. proxy_header  

* nginx는 디폴트로 요청에 대하여 두 가지의 헤더를 추가한다.  

#### 1. Host : $proxy_host  
#### 2. Connection : "Close"  
* **keep-alive**를 배제한다.  

* **proxy_set_header**를 통하여 **커스튬 해더**를 
```
location /auth {
  proxy_set_header X-custom-header "hihi"
  proxy_pass http://127.0.0.1:8007;
}
```













