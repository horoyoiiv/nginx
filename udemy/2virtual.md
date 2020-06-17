

# Creating a Virtual Host  


* `http context` 안에 `server context`를 만든다.  
* 각각의 `server context`는 하나의 **virtual host**를 의미한다.  

## 1. virtual host  

* `server context`로 정의된 각각의 **virtual host**는 **특정 포트**를 통해 listening할 `책임`을 가진다.  

```
events { }

http {
    
    server {    # server context로 정의된 virtual host 
        
        listen 80;
        server_name 127.0.0.1;
        
        root /sites/demo;
    }
}
```
이는 해당 `virtual host`는 port 80으로 listening하며, **server_name**은 IP 혹은 domain name이 올 수 있으나,  
위의 경우 IP 주소를 적었다.  


## 2. static contents serving을 위한 root directive  

#### 2.1. 제공할 static file  
* `/sites/demo` path에 저장되어 있다.  
```
/sites/demo$ tree
.
├── index.html
├── style.css
└── thumb.png
```

#### 2.2. root directive 사용  
```
root /sites/demo;
```
위와 같이 설정할 경우 http://domain.com/images/cat.png 라는 요청이 들어왔을 때,  
**설정된 root directory path + urld의 path 를 concat**하여 파일을 찾는다.  

```
events { }

http {
    
    server {
        
        listen 80;
        server_name 127.0.0.1;
        
        root /sites/demo;       // target directory 를 설정
    }
}
```

![스크린샷, 2020-06-17 16-48-35](https://user-images.githubusercontent.com/62331555/84870550-6ac62e80-b0ba-11ea-910d-aaa802e2367c.png)   
위의 요청에 대하여 nginx는 /sites/demo/images/cat.png 파일을 찾는 것이다.  


#### 2.3. contents-type 설정하기  
* 단순히 다음과 같이 설정을 하게 된다면 
```
events { }

http {
    server {
        
        listen 80;
        server_name 127.0.0.1;
        
        root /sites/demo;       // target directory 를 설정
    }
}
```

* 아래와 같이 css 파일은 200 OK로 응답되지만, **Contents-Type**이 **text/plain**이기에 제대로 랜더링되지 않는다.  
![스크린샷, 2020-06-17 16-57-50](https://user-images.githubusercontent.com/62331555/84871613-b75e3980-b0bb-11ea-97be-80f999d5290e.png)  

#### 2.4. mime type 설정하기 (1)    
* 아래와 같이 **types context**에 **확장자**에 따른 **mime type**을 지정할 수 있다.  
```
events { }

http {
    
    types {
        text/html html;   // 확장자가 html 이라면, contents-type의 mime type에 text/html 을 추가.
        text/css css;     // 확장자가 css 이라면,  contents-type의 mime type에 text/css  을 추가.
        text/hello jpeg   // 확장자가 jpeg 이라면, text/hello 라는 사용자가 지정한 type을 넣을 수도 있다.
    }

    server {
        
        listen 80;
        server_name 127.0.0.1;
        
        root /sites/demo;       // target directory 를 설정
    }
}
```

#### 2.5. mime type 설정하기 (2)  
* 하지만 하나 하나 추가하기 보다는 nginx가 제공하는 mime types 파일을 include할 수도 있다.  
* **mime.types** 파일은 /etc/nginx 아래에 저장된 파일이다.  
* 이 파일의 내용은 아래와 같다.  
```
// /etc/nginx/mime.types
types {
    text/html                             html htm shtml;
    text/css                              css;
    text/xml                              xml;
    image/gif                             gif;
    image/jpeg                            jpeg jpg;
    application/javascript                js;
    application/atom+xml                  atom;
    application/rss+xml                   rss;

    text/mathml                           mml;
    text/plain                            txt;
    text/vnd.sun.j2me.app-descriptor      jad;
    ...
```

* 그리고 이 파일 자체를 configuration file에 **include**시켜준다.  
```
events { }

http {
    
    include mime.types;     // mime.types 파일을 상대경로로 추가했다.

    server {
        
        listen 80;
        server_name 127.0.0.1;
        
        root /sites/demo;       // target directory 를 설정
    }
}
```

* 그 결과 아래와 같이 브라우져는 파일의 **확장자**에 알맞는 **mime type**을 가진 응답을 받게 된다.  
![스크린샷, 2020-06-17 17-08-03](https://user-images.githubusercontent.com/62331555/84872651-225c4000-b0bd-11ea-9906-6b6e5e2f2c4a.png)  



