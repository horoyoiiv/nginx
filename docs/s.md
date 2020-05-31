

# static  

* `/etc/nginx/nginx.conf` : configuration 파일을 통해 nginx를 설정한다.  

## 1. static contents를 제공하는 가상 호스트 설정  

#### [root 디렉티브란?](https://docs.nginx.com/nginx/admin-guide/web-server/serving-static-content/)  

1. `server` 디렉티브를 통해 `가상 호스트`를 설정한다.  
2. `listen`을 통해 `포트`를 설정한다.  
3. `server_name`을 통해 도메인 네임을 설정한다.  
4. **root** : 파일을 탐색할 **루트 디렉토리**를 설정한다.  

```
http {
    
    # virtual host 1

    server {
        listen 80;
        server_name naver.com;

        root /var/html;       // 파일을 탐색할 "루트" 디렉토리 지정.
    }
}
```

* 위의 경우 `127.0.0.1:80/hello.html` 이라는 요청이 들어오면  
root에 지정된 `/var/html` 뒤에 `/hello.html`이라는 **path**을 append하여 해당 파일을 찾는다.  
* `127.0.0.1/hello.html`은 /var/html/hello.html 을 조회하게 됨.  


## 2. location 을 통핸 특정 URI을 지정하기  
* location 디렉티브를 통하여 **특정 URI의 path**를 처리하도록 설정한다.  
* `location` 뒤에는 **prefix match**를 지정한다.  
```
server {

  locatoin /images {
      return 200 'such a good day';
  }
}
```

* 이후 지정된 `prefix` 시작하는 모든 URI은 이를 통해 처리된다.  
* 아래의 요청 모두 location /images 가 처리한다.  
```
http://127.0.0.1/images
http://127.0.0.1/images/awef
http://127.0.0.1/images/hello/world
```

## 3. exact match 사용하기  
* = `대입 연산자`를 추가하여, 해당 path에만 서빙하도록 지정할 수 있다.  

```
server {

  locatoin = /images {
      return 200 'such a good day';
  }
}
```

```
http://127.0.0.1/images
http://127.0.0.1/images/awef      // 안됨
http://127.0.0.1/images/hello/world // 안됨
```

## 4. location /images 를 통한 이미지 서빙  
* root : 파일을 찾을 `루트 디렉토리`  
```
location /images {
    root /var/www;  
}
```
* 아래와 같은 요청이 발생하면  
```
127.0.0.1:80/images/img.png
아래를 찾게 된다.

/var/www/images/imp.png
```
* URI에서 path 앞의 부분이 /var/www로 대체된다.  









