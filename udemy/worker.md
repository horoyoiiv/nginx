# workder process  

```
systemctl status nginx
```

![스크린샷, 2020-06-23 13-43-49](https://user-images.githubusercontent.com/62331555/85361720-a4ce7f00-b557-11ea-8f12-36c8a529a0bc.png)  

* **master process** : 실제로 실행되는 nginx 서비스  
* **worker process** : master로부터 `spawn`되어서, 유정의 요청을 듣고 응답하는 프로세스  
* default는 하나의 프로세스 생성  


## 1. 생성하기  

```
events {}

user www-data;    // 해당 프로세스를 실행시킬 사용자를 지정한다. 

worker_processes 8; // worker 프로세스의 수를 8개로 지정한다.

```
* user가 www-data인 8개의 worker process가 생성된다.  

```
$ ps aux | grep nginx

root      1122  0.0  0.0  33332  3472 ?        Ss   13:40   0:00 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
www-data  4862  0.0  0.0  37884  3872 ?        S    13:47   0:00 nginx: worker process
www-data  4863  0.0  0.0  37884  3868 ?        S    13:47   0:00 nginx: worker process
www-data  4864  0.0  0.0  37884  3852 ?        S    13:47   0:00 nginx: worker process
www-data  4865  0.0  0.0  37884  3872 ?        S    13:47   0:00 nginx: worker process
www-data  4866  0.0  0.0  37884  3884 ?        S    13:47   0:00 nginx: worker process
www-data  4867  0.0  0.0  37884  3884 ?        S    13:47   0:00 nginx: worker process
www-data  4868  0.0  0.0  37884  3884 ?        S    13:47   0:00 nginx: worker process
www-data  4869  0.0  0.0  37884  3884 ?        S    13:47   0:00 nginx: worker process
```

## 2. [최적화] 워커 프로세스의 수는 몇으로?  
* 코어의 수에 맞게 설정  

#### 2.1. 코어의 수를 확인  

```
$ nproc
$ lscpu
```

#### 2.2. 
* `auto`로 세팅 시, cpu당 하나의 worker를 생성한다.  
```
worker_processes auto;
```

## 3. [최적화] connection 수  

* 하나의 `worker process` 당 열 수 있는 **파일의 수**  
* 하나의 프로세스 당 열 수 있는 파일의 수  
```
$ ulimit
1024
```

<br/><br/>
```
events {
  worker_connections 104;
}
```

## 4. pid 설정  
* 현재 실행되고 있는 nginx의 pid가 저장된 파일  
```
/var/run/nginx.pid
```
</br></br>

* 아래와 같이 configuration file에 추가하여, pid 파일을 바꿀 수 있다.  
```
 pid /var/run/new_nginx.pid
```




















