# Buffering    
* 
```
http {

  # Buffer size fo POST submission.
  client_body_buffer_size 10K;
  client_max_body_size 8m;        # 8megabytes : body의 크기가 이 이상되면 413 응답


  # Buffer size for header
  client_header_buffer_size 1k;
  
  
  # Max time to receive client headers/body
  client_body_timeout 12;   # ms 단위 : 연속되는 read operation의 시간 차
  client_header_timeout 12s; # 초 단위
  
  # max time to keep a connection open for
  keepalive_timeout 15;
  
  # Max time for the client receive a response.
  send_timeout 10;
  
  # skip buffering for static files 
  sendfile on;
  
}
```
