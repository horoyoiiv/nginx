

## image를 따로 서빙하는 path를 생성.  


### 1. location /prefix  

* 이와 같은 요청은 url의 path의 prefix가 일치하는 경우 해당 디렉토리에서 파일을 서빙.  
```
http {

    server{
        listen 8080;
        root /var/www/html;
        
        location /images {
            root /var/www;
        }
    }
}

```

### 2. 디렉토리와 위치 매핑하기  
* 
```
// /var/www/images 디렉토리
img.png
```

```
http://localhost:8080/images/img.png
```







