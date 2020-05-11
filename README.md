# nginx  

## [유튜브 크래시 코스!](https://www.youtube.com/watch?v=WC2-hNNBWII&t=2629s)  
## [굿 사이트(very)](https://velog.io/@minholee_93/Nginx-Worker-Process-6jk61i2gmm)  

nginx
## [1. 기본 용어](/all/what.md)  
* **Web Server** and **WAS**
* L4 Load Balancer 와 L7 Load Balancer  

## [2. NginX의 구조](/all/tuto.md)  
* 하나의 마스터 프로세스와 여러 대의 **워커 프로세스**로 이뤄진다.  
* 각 워커 프로세스는 정해진 갯수의 **커낵션**을 관리한다.  

## [3. static 자원 서빙하기](/all/ws.md)  
* 파일 자체에 대한 other의 **read** 옵션 부여  
* 디렉토리에 대한 other의 **read**와 **exec** 옵션 부여  
- 디렉토리의 (r)은 list를 볼 수만 있음. (e)부여 시 접근 가능.  

## [4. location /prefix 를 통한 sub path 설정](/all/sub.md)  




#### 1. install nginx 
[우분투에 nginx 설치하기](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-18-04)  

#### 2. 상태 확인  

![스크린샷, 2020-04-19 16-34-46](https://user-images.githubusercontent.com/62331555/79682267-b8a9ec00-825b-11ea-9484-d1053b03edb2.png)  

1. daemon으로서, 포트 80에서 동작.  
작동하지 않는다면, 이미 apache가 설치되어 포트 80을 쓰고 있는지 의심  

#### 3. nginx 설정  

**etc/nginx/nginx.conf** 파일에서 설정  

#### 4. 로드밸런싱하기  
[](https://kamang-it.tistory.com/entry/WebServernginxnginx%EB%A1%9C-%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%8B%B1-%ED%95%98%EA%B8%B0)  


#### 5. static file caching하기  



