# log  
* error log  
* access log  

#### 기본 path  
```
/var/log/nginx/error.log
/var/log/nginx/access.log
```

<br/><br/>
#### access log example 

```
127.0.0.1 - - 
[19/Jun/2020:21:44:47 +0900] 
"GET /thumbb.png HTTP/1.1" 404 580 
"-" "Mozilla/5.0 (X11; Linux x86_64) 
AppleWebKit/537.36 (KHTML, like Gecko) 
Chrome/80.0.3987.149 Safari/537.36"  
```

## 1. Custom Log  

* Using **access_log**, You can generate a custom log file in the path you want.  
```
location /secure {
    access_log /var/log/nginx/custom.log; 
    return 200 "This is a secure area.";
}
```

## 2. Disable log  
* generating log files can be **disable** by using of **access_log off**;  
* In this way, performance can be higher.  

```
location /secure {
    access_log off;
    return 200 "This is a secure area.";
}
```


