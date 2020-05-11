
# NginX 구조  

* apache는 **connection**마다 **프로세스** 혹은 **쓰레드**를 생성한다.  
* nginx는 **master 프로세스** 하나와 **worker process** 여러 대를 가지며 각 워커가 고정 크기의 connection을 비동기적으로 담당.  


## 1. NginX의 방식 - 워커 프로세스 갯수   
* **비동기 IO를 활용**한, **event driven방식**으로 **고정된 워커 프로세스**가 각 io를 관리.  

* systemctl로 확인해보면, **master 프로세스**아래에 **work process**가 여러개 위치한다.  
![스크린샷, 2020-05-11 18-35-20](https://user-images.githubusercontent.com/62331555/81547035-34f4a280-93b6-11ea-8688-afa87e65fcfd.png)  
* 디폴트는 **8개**  
* 아래와 같이 설정으로 통해 워커 프로세스 갯수 제한 가능.  
```
/etc/nginx/nginx.conf  

worker_processes 3;
```

![스크린샷, 2020-05-11 18-42-28](https://user-images.githubusercontent.com/62331555/81547701-2fe42300-93b7-11ea-9c95-d228ec4ffd49.png)  

### (결론) NginX는 비동기 방식이기에, 자신의 CPU core 수만큼 worker process를 생성하면 된다.  


## 2. 워커 프로세스 당 커넥션의 갯수  

* 하나의 프로세스가 open할 수 있는 파일의 개수 : soft  
```
$ ulimit -n
1024
```

```
/etc/nginx/nginx.conf  

events {
  workder_connections 1024;     // 하나의 워커 당 1024개의 커넥션을 동시에 다룰 수 있도록 설정. 
}
```

















