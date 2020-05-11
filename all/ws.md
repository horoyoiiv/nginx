

# Web Server로서의 NginX 세팅  

* Web Server로서라면 static contents 서빙을 위한 프로그램  

## 1. access 혹은 error log 파일.  

* nginx는 하나의 프로그램으로서, 실행 중 발생한 로그들을 **/var/log/nginx** 하위에 저장한다.  

```
/var/log/nginx 하위

access.log
error.log
```

## 2. html 파일 서빙  
* 8080으로 들어온 요청에 대하여 /var/www/html/ 하위 **static 자원을 서빙**하겠다.  

```
http {

    server{
        listen 8080;
        root /var/www/html/;            // 해당 디렉토리 밑의 자원을 제공.
    }
}
```

* 해당 디렉토리 안에는 다음과 같은 자원이 있다.  
```
// /var/www/html
hello.html
index.html
index.nginx-debian.html
```
* 아래와 같이 URL을 요청하면, path는 곧 호스트 서버의 특정 디렉토리에 매핑되고, 그 안의 파일을 제공한다.  
```
http://localhost:8080/index.nginx-debian.html
http://localhost:8080/hello.html
http://localhost:8080/index.html
```
* **http://localhost:8080/** 은 **/var/www/html/** 와 매핑.  

## 3. 하위 패쓰 설정  

#### 3.1. 해당 root 경로는 그대로  
```
http {

    server{
        listen 8080;
        root /var/www/html/;
    }
}

```
#### 3.2. 해당 디렉토리 안에서 서브 디렉토리를 만든다.  
* 해당 서브디렉토리가 곧 **URL의 하위 path**가 된다.  
* 두 디렉토리 생성  
```
// var/www/html 디렉토리 아래에
site1     
site2     
```

#### 3.3. 하위 디렉토리 아래에 index.html 생성  
* 다음과 같은 URL 요청 시 /var/www/html/site1/index.html 이라는 정적 자원을 서빙해준다.  
```
http://localhost:8080/site1/
http://localhost:8080/site2/
```

#### 3.4 권한  

* NginX를 통해 서빙하고자하는 파일은 **other - read 권한**이 필요하다.  
* 그 파일을 포함하는 디렉토리들은 그 파일을 읽을 수 있어야 하기에 **other - executable 권한**이 필요하다.











