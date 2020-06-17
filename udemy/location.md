
# location  

* **요청을 인터셉터한다.**  
* **location** directive는 특정 **URI**에 대하여 어떻게 동작할지를 설정한다.  


![스크린샷, 2020-06-18 04-01-26](https://user-images.githubusercontent.com/62331555/84938846-8829e580-b118-11ea-9382-48ad8f51fa64.png)  

<br/><br/>
 

아래의 경우 단순히 URI의 path를 빼내와서 file을 서빙했다.  
```
    server {
        
        listen 80;
        server_name 127.0.0.1;
        
        root /sites/demo;
    } 
```
<br/><br/>

* location을 사용하면 특정 URI에 대한 다른 처리가 가능해진다.  
```
    server {
        
        listen 80;
        server_name 127.0.0.1;
        
        root /sites/demo;
        
        location /greet {
          return 200 "Hello from me!"       # 두 가지의 인자를 받는다.
        }
        
    } 
```
<br/><br/>

## 1. prefix match 형  

```
location /greet {
  return 200 "Hello from me!"       # 두 가지의 인자를 받는다.
}
```
* prefix mathc 형이기에 /greet으로 시작하는 모든 URI를 처리한다.  
* 아래는 모두 위와 매치되는 URI 패턴이다.  
```
http://mydomain.com/greet
http://mydomain.com/greeting
http://mydomain.com/greets
http://mydomain.com/greet/more
```

<br/><br/>
## 2. exact match 형  
* **=**를 앞에 붙인다.  

```
location = /greet {
  return 200 "Hello from me!"       # 두 가지의 인자를 받는다.
}
```
* =를 붙여서 딱 맞게 설정가능해진다.  
```
http://mydomain.com/greet
```

<br/><br/>

## 3. regex match 형  
* 정규표현식을 적용하여 URI 패턴을 등록할 수 있다.  
* PCRE Lib을 포함시킨 이유이다.  

* **~** 정규표현식 사용을 의미한다.  
* case-sensitive한 경우이다.  
```
location ~ /greet[0-9] {
  return 200 "Hello from me";
} 
```
<br/><br/>
```
[x]http://mydomain.com/greet
[o]http://mydomain.com/greet2
[o]http://mydomain.com/greet3/ping
[o]http://mydomain.com/greet1/pong
```

* 이 경우에도 **prefix**처럼 동작하기에 Line end를 알리는 **$**를 추가하면 exact처럼 동작할 수 있다.  
```
location ~ /greet[0-9]$ {
  return 200 "Hello from me";
} 
```
<br/><br/>
* 또한 * 을 추가하여 case-insensitive하게 만들 수 있다.  

```
location ~* /greet[0-9]$ {
  return 200 "Hello from me";
} 
```

## 4. Preferential Prefix 형  
* 원래는 regex 형보다 prefix형의 우선순위가 낮지만 ^~ 을 사용하여 우선순위가 더 높은 prefix형을 만들 수 있다.  

```
location ^~ /greet {          # 이것이 먼저 서빙된다.
  return 200 "Hello from me";
}

location ~* /greet {
  return 200 "Hello from me";
}

```



## 5. location 패턴의 우선순위  

![스크린샷, 2020-06-18 04-24-36](https://user-images.githubusercontent.com/62331555/84941054-be1c9900-b11b-11ea-9bb4-7a91e7ff2ef0.png)  














