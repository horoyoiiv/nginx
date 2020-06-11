
# health check  
#### [nginx docs](https://docs.nginx.com/nginx/admin-guide/load-balancer/http-health-check/)  

# Introduction  
nginx는 지속적으로 `upstream server`를 테스트하여, failed된 서버를 피하고 recovered된 서버를 다시 추가한다.  

* Passive health check : 응답을 모니터링하여, upstream 서버의 상태를 판단한다.   
* Active health check : 직접 요청을 보내서 upstream 서버의 상태를 판단한다.  


# Passive Health Check  

* nginx는 `upstream server`와의 transaction을 모니터링하여 실패 시 **일시적으로** 해당 upstream 서버로의 요청 전송을 중지한다.  
* 이후 **active**로 다시 mark되면 요청을 전송한다.  

* `fail_timeout` :  두 가지의 의미를 가진다.  
[+] upstream 서버가 `unavailable`되었을 때, recover되기까지 기다리는 시간.  
[+] 이 시간 안에 max_fails에 정의된 횟수만큼 fail 발생 시 `unavailable`로 마킹한다.  

* `max_fails` : `fail_timeout` 시간 내에 발생해야 하는 fail의 수 to  be marked unavailable.   

```
upstream backend {
    server backend1.example.com;
    server backend2.example.com max_fails=3 fail_timeout=30s;
}
```

# Active Health Check  

