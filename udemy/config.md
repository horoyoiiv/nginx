

# 1. 용어  
* Configuration file 내에서 두 가지의 용어가 사용된다.  
1. **context**  
2. **Directive**  


## 1.1. Context  
* 일종의 **scope**다.  
* context는 nested가 가능하며, inherited된다.  
* 아래의 경우 `http` context 안에 `server` context가 있다.  

#### 1.1.1. 예제  
![스크린샷, 2020-06-17 14-48-00](https://user-images.githubusercontent.com/62331555/84860214-a1477d80-b0a9-11ea-9fbc-1d654a6ff725.png)  
* **http context** 내에서 http와 관련된 **설정**을 정의한다.  
* http context 안의 **server context** 내애서는 **virtual host**를 정의힌다.  
* http context 안의 server context 안의 **location context**에서는 들어오는 요청의 URI location을 매칭하기 위해 사용.  



## 1.2. Directive  

* **name과 value** pair로 구성된다.  
```
server_name mydomain.com
```
