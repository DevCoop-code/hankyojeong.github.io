---
title: "라즈베리파이를 이용한 RTMP 스트리밍"
date: 2020-07-12 18:00:00
categories: mediaStreaming
---

# RTMP 스트리밍 서버 구축 방법
라즈베리파이, PiCam 그리고 nginx-rtmp 서버를 이용하여 RTMP 스트리밍 서버를 구축.

## 사용한 HW 및 SW
1. 라즈베리 파이 3
2. PiCam
3. nginx-rtmp
4. ffmpeg
5. Docker
6. VLC player

## 라즈베리파이에 Docker 설치
1. Docker 설치 Shell script 다운
   1. curl -fsSL get.docker.com -o get-docker.sh
2. get-docker.sh 실행
   1. sudo bash get-docker.sh
3. Docker 서비스 동작 확인
   1. ps auwx|grep docker
4. Docker 프로세스 확인
   1. ps auwx|grep docker
5. 일반계정으로 docker 사용하게 하기
   1. sudo usermod -aG docker pi
6. nginx-rtmp docker source download
   1. wget https://github.com/brocaar/nginx-rtmp-dockerfile/archive/master.zip
7. 압축을 해제하고 nginx-rtmp폴더 내부에 config 폴더를 생성
   1. unzip master.zip
   2. cd nginx-rtmp-dockerfile-master/
   3. mkdir config
8. Docker instance의 timezone 설정을 위해 config 폴더에 RPi의 /etc/localtime 파일을 복사
   1. cp /etc/localtime nginx-rtmp-dockerfile-master/config
9. nginx.conf 파일 내용을 수정하여 config 폴더에 복사, 복사하기 전 서버에서 인코딩 하는것이 아닌 클라이언트에서 인코딩 후 서버에서는 단순 전송만을 수행하기 위해 nginx.conf 파일을 수정
   1.  ![rtmp_Image](https://hankyojeong.github.io/assets/images/20200712/nginxconf.png)
   2.  cp nginx.conf config
10. Dockerfile 수정 - docker image의 기본이 되는 OS를 Trusty에서 resin/rpi-raspbian으로 변경
    1.  sudo vi Dockerfile
    2.  FROM ubuntu:trusty   ->   resin/rpi-raspbian
    3.  ffmpeg build 부분은 주석처리
        1.  ![rtmpffmpeg_Image](https://hankyojeong.github.io/assets/images/20200712/dockerfile_ffmpeg_fix.png)
    4.  nginx.conf 복사는 하지 않도록 주석 처리
        1.  ![rtmpcp_Image](https://hankyojeong.github.io/assets/images/20200712/dockerfile_cp_fix.png)
11. nginx-rtmp build
    1.  docker build -t nginx-rtmp .
12. nginx_rtmp image 파일이 제대로 등록되었는지 확인
    1.  docker images
13. nginx-rtmp docker instance 실행
    1.  config 폴더에 복사한 2개의 파일을 mapping에 추가하여 실행
    2.  sudo docker run --name nginx-rtmp -p 1935:1935 -p 8080:80 -v /home/pi/nginx-rtmp-dockerfile-master/config/nginx.conf:/config/nginx.conf -v /home/pi/nginx-rtmp-dockerfile-master/config/localtime:/etc/localtime nginx_rtmp
14. docker 확인
    1.  docker ps
15. RTMP 송출하기
    1.  sudo raspivid -w 1280 -h 720 -t 0 -b 1500000 -fps 20 -o - | ffmpeg -y -f h264 -i - -c:v copy -an -f flv -rtmp_buffer 100 -rtmp_live live rtmp://localhost:1935/live/101