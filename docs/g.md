

# gzip  

* `응답`을 `gzip`으로 **압축하여** 클라이언트에 전송한다.  

## 1. gzip  
** GNU zip **

## 2. 흐름  

#### 1. 클라이언트에서 "자신은 gzip을 처리할 수 있음!"을 알려준다.  
* 이는 요청헤더에 **Accept-Encoding** 필드에 **gzip**을 추가하여 가능하다.  

```
// 요청 헤더
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Accept-Encoding: gzip, deflate, br  // 클라이언트가 gzip 포멧을 처리할 수 있음을 알려준다.
```

#### 2. 서버는 이를 확인한 후 "제공할 응답을 압축"하여 전달한다.  

```

http {
    
    # virtual host 1
    server {
        include mime.types;
        
        gzip on;                          // gzip 을 사용한다.
        gzip_comp_level 8;                // 압축 정도를 설정한다. 3~4 정도가 적당하다.
        gzip_types image/png video/mp4;   // gzip을 적용할 데이터 타입을 설정

        ...
```

* gzip 적용 후 미세하게 용량이 줄어들었다.
* **png**의 경우 이미 압축된 형태이기 때문이다.  

```
// gzip 적용 전-----------------
curl http://127.0.0.1:80/images/img.png > img.png
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  [6485]  100  6485    0     0  6333k      0 --:--:-- --:--:-- --:--:-- 6333k

// gzip 적용 후----------------
curl -H "Accept-encoding: gzip" http://127.0.0.1:80/images/img.png > img.png
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  [6393]    0  6393    0     0  6243k      0 --:--:-- --:--:-- --:--:-- 6243k
```
