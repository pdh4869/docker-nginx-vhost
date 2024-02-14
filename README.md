# docker nginx vhost

## Dockerfile
```
FROM nginx
COPY index.html /usr/share/nginx/html
```
<hr />

## Build & Run
```
sudo docker build -t n-s-2:0.1.0 . -f Dockerfile  // serv-a
sudo docker build -t n-s-3:0.1.0 . -f Dockerfile  // serv-b
sudo docker build -t n-s-4:0.1.0 . -f Dockerfile  // lb

sudo docker run -d --name s2-1 -p 9002:80 n-s-2:0.1.0  // serv-a
sudo docker run -d --name s3-1 -p 9003:80 n-s-3:0.1.0  // serv-b
sudo docker run -d --name lb-1 -p 9004:80 n-s-4:0.1.0  // lb

// sudo docker run -d --name ~ --network aaa ~ 등 network를 지정함으로써 network connect 생략 가능함.

```

<hr />

## Network 
```
sudo docker network create aaa

sudo docker network connect aaa s2-1  // serv-a
sudo docker network connect aaa s3-1  // serv-b
sudo docker network connect aaa lb-1  // lb

sudo docker network inspect aaa // aaa에 세 컨테이너가 잘 묶였는지 확인
```
![image](https://github.com/pdh4869/docker-nginx-vhost/assets/76561901/78d313a3-7d16-42af-95d1-08cc2ace8add)

<hr />

### 결과 
![image](https://github.com/pdh4869/docker-nginx-vhost/assets/76561901/582a8260-fee3-4e8b-881d-c6d4e14a86b6)

<br /> <br /> <br/>

![image](https://github.com/pdh4869/docker-nginx-vhost/assets/76561901/85872bb2-86d4-4c98-8c11-d3a2a8954ee7)
