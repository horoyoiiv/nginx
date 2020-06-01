# nginx  

## [유튜브 크래시 코스!](https://www.youtube.com/watch?v=WC2-hNNBWII&t=2629s)  
## [굿 사이트(very)](https://velog.io/@minholee_93/Nginx-Worker-Process-6jk61i2gmm)  

# 역할  
#### 1. static file에 대한 서빙  
#### 2. 


# [1. static contents](/docs/s.md)  
* `WAS`까지 가지 않고, `Reverse Proxy` 단에서 `정적 컨텐츠(html, css, img)`를 제공할 수 있다.  
![스크린샷, 2020-05-31 10-54-25](https://user-images.githubusercontent.com/62331555/83342681-23574880-a32d-11ea-8431-0e2100558c42.png)  
###### [출처](https://medium.com/@francoisromain/setup-node-js-apache-nginx-reverse-proxy-with-docker-1f5a5cb3e71e)  

```
http {
  server {  // 호스트 서버 위에서 동작하는 가상 호스트1
    listen 80;
    server_name example.com;
  
    root /var/html;         // 파일을 찾을 루트 디렉토리 : 호스트의 해당 DIR 아래는 html 파일이 저장.
  
    location /images {      // path의 prefix가 /images/* 라면 /var/www/images/* 에서 자원 찾는다.
        root /var/www;    
    }
  }
}
```

### TODO : dynamic contents가 포함된 html은 was에서, css는 ws에서 제공하기  

# [2. nginx의 로그 관리](/master/docs/l.md)  
* /var/log/nginx 디렉토리 아래에서 access.log 혹은 error.log 가 저장된다.  
* 향후 사용자 분석, 디버깅 등에 사용될 수 있다.  

# [3. nginx단에서 헤더 추가](/master/docs/h.md)  
```
location /path {
    add_header Cache-Control public;
    expires 10m;
}
```
# [4. reverse proxy](/master/docs/r.md)  
* `/auth` path를 가지는 요청이 들어오면 `proxy_pass` 에 기입된 upstream 서버로 요청을 포워딩한다.  
* **Connection** 필드는 **Close**로 세팅되어 전달된다.  

```
location /auth {
  proxy_set_header X-Header "good";   // 커스튬 헤더 추가 가능.
  proxy_pass http://127.0.0.1:8007;
}
```

# [4. 응답 캐싱]  
# [5. 로드 밸런싱]  





























nginx
## [1. 기본 용어](/all/what.md)  
* **Web Server** and **WAS**
* L4 Load Balancer 와 L7 Load Balancer  

## [2. NginX의 구조](/all/tuto.md)  
* 하나의 마스터 프로세스와 여러 대의 **워커 프로세스**로 이뤄진다.  
* 각 워커 프로세스는 정해진 갯수의 **커낵션**을 관리한다.  

## [3. static 자원 서빙하기](/all/ws.md)  
* 파일 자체에 대한 other의 **read** 옵션 부여  
* 디렉토리에 대한 other의 **read**와 **exec** 옵션 부여  
- 디렉토리의 (r)은 list를 볼 수만 있음. (e)부여 시 접근 가능.  

## [4. location /prefix 를 통한 sub path 설정](/all/sub.md)  




#### 1. install nginx 
[우분투에 nginx 설치하기](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-18-04)  

#### 2. 상태 확인  

![스크린샷, 2020-04-19 16-34-46](https://user-images.githubusercontent.com/62331555/79682267-b8a9ec00-825b-11ea-9484-d1053b03edb2.png)  

1. daemon으로서, 포트 80에서 동작.  
작동하지 않는다면, 이미 apache가 설치되어 포트 80을 쓰고 있는지 의심  

#### 3. nginx 설정  

**etc/nginx/nginx.conf** 파일에서 설정  

#### 4. 로드밸런싱하기  
[](https://kamang-it.tistory.com/entry/WebServernginxnginx%EB%A1%9C-%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%8B%B1-%ED%95%98%EA%B8%B0)  


#### 5. static file caching하기  



