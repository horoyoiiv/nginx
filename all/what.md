
# NginX 란 무엇인가?  

* **Web Server**이다.  
* 동시에 **reverse proxy**이다.  
  
  
1. Web Server로서, Web application Server 클러스터 앞 단에 배치되어  
2. **Reverse Proxy**로서, Client요청을 받아들인 후, **upstream 서버에 포워딩하는 역할**을 담당.  
3. 혹은 로드 밸런싱을 수행하여, Client의 요청인 Workload를 분산한다.  
3. 혹은 static 자원 등에 대한 **caching** 기능을 제공.  


* non-threaded이자 event-driven 방식.  

## 1. Web Server vs Web Application Server  
#### [WS vs WAS](https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html)  

#### 1.1. Web Server   
클라이언트의 요청을 받아 **static contents**를 제공하는 프로그램.  

#### 1.2 Web Application Server   
WAS는 **Web Server의 기능**에 더하여, DB와 연동되어 비즈니스 로직까지 수행하여 **dynamic content**를 수행할 수 있는 프로그램  

#### 1.3. 결론  
1. **Web Server** : 클라이언트의 요청에 대하여 html 등의 **static contents**를 제공하는 프로그램  
2. **Web Application Server** : 정적 자원뿐만 아니라, **dynamic contents**까지 서빙할 수 있는 프로그램  

* 왜 두 가지를 나누어 쓰는가?  
1. WAS의 부하분산 : 간단한 static file은 앞단에 캐싱하여 빠르게 응답.  
2. 두 개의 이상의 upstream에 대한 load balacing을 Web Server가 수행.  
3. Web Server 앞 단에서 SSL 암-복호화를 대신 수행.  


![스크린샷, 2020-05-11 18-04-16](https://user-images.githubusercontent.com/62331555/81544019-daf1de00-93b1-11ea-8202-aa0d27b18b60.png)  

## 1. L4 Load Balancer 와 L7 Load Balancer  
#### [L4 vs L7 ](https://levelup.gitconnected.com/l4-vs-l7-load-balancing-d2012e271f56)  

* L4 LB : 클라이언트의 요청의 정보 중 L4 이하의 정보 - IP와 Port를 기반으로 포워딩을 수행.  
* 그렇기에 상위 데이터인 payload를 보지 않는다.  

![스크린샷, 2020-05-11 18-14-17](https://user-images.githubusercontent.com/62331555/81545016-3f616d00-93b3-11ea-9bac-8cd1ff4b41fd.png)   

* L7 LB : L7까지, 그러니까 HTTP의 헤더의 정보까지 보면서, 이를 바탕으로 포워딩할 서버를 선택.  

# NginX 구성  
































