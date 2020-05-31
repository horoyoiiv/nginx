
# nginx의 로그 관리  

* **/var/log/nginx** 하위에 저장된다.  

#### 1. access.log  
* nginx에 대한 접근 기록을 로그로 남긴다.  

```
127.0.0.1 - - [31/May/2020:10:08:10 +0900] "GET /hello.html HTTP/1.1" 200 51 "-" "Mozilla    /5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.149 Safa    ri/537.36"
127.0.0.1 - - [31/May/2020:10:10:13 +0900] "GET /hellos.html HTTP/1.1" 404 580 "-" "Mozil    la/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.149 Sa    fari/537.36"
```

#### 2. error.log  
* nginx와 관련된 error 로그가 기록된다.  
1. 요청을 제대로 처리하지 못 한 경우  
2. configuration file이 invalid한 경우  
```
2020/05/31 10:10:13 [error] 10440#10440: *23 open() "/var/www/html/hellos.html" failed (2    : No such file or directory), client: 127.0.0.1, server: naver.com, request: "GET /hellos    .html HTTP/1.1", host: "127.0.0.1"
```

