---
title: "미디어 프로그래밍을 위한 기초지식"
date: 2021-01-05 09:43:00
categories: mediaKnowledge
---

# 미디어 프로그래밍을 위한 기초지식
미디어 프로그래밍을 위해 필요한 기초 지식

### Frame Rate?
Frame은 동영상을 이루는 여러 이미지 중 하나의 정지된 이미지를 의미

초당 Frame 갯수 = Frame Rate, 단위: fps

### 화면 주사 방식
- 비월 주사(Interlacing)
  - 한번에 모든 화면을 보내지 않고 홀수 줄과 짝수 줄을 나눠서 보냄
    - 실제 전송 Frame은 절반으로 줄어들지만 사람 눈의 착시로 인해 느끼지 못함
  - But, 영상이 급격한 움직임을 보이면 잔상이 남음(= Interlace Noise)
  - 비월 주사 방식은 현재는 거의 쓰이지 않음

- 순차 주사(Progressive)
  - 영상을 한 번에 하나의 Frame으로 전송

### 크로마 서브샘플링
사람의 눈은 밝기 차이는 민감하지만 색상 차이에는 상대적으로 둔감함

크로마 서브샘플링은 사람의 눈에 둔감한 색차 정보는 줄이고 민감한 명도를 기반으로 영상을 압축하는 방식

동영상을 이루는 Frame의 색을 표현하는 방법에는 RGB가 있지만 하나의 Pixel을 표현하는데 24bit(한 색당 8bit)를 사용하는데는 많은 용량이 필요했음

YUV는 빛의 양을 정하는 휘도(Y)와 색차(U,V)를 사용함. Digital에서는 U와 V 대신 파랑(Cb)과 빨강(Cr)을 사용함

Example) YUV444, YUV422, YUV420 <- 4개의 Pixel을 기준으로 얼마나 많은 양의 U와 V를 어떻게 사용하는지에 따라 결정



### 컨테이너(Container)
![mediaContainer](https://hankyojeong.github.io/assets/images/mediaBasicKnowledge/videoContainer.png)

- 멀티플렉싱(Multiplexing), 먹싱(Muxing)
  - 캡쳐된 비디오와 녹음된 오디오를 저장하기 위해 이들 스트림을 컨테이너에 담는 일련의 과정
- 디멀티플렉싱(Demultiplexing), 디먹싱(Demuxing)
  - 컨테이너에 있는 스트림을 Container에서 분리하는 일련의 과정

### 코덱(Codec)
아날로그 신호 혹은 스트림 데이터로 이뤄진 비디오와 오디오를 압축된 부호로 변환하기 위한 압축 규격

![codec](https://hankyojeong.github.io/assets/images/mediaBasicKnowledge/codec.png)

### 픽셀(Pixel)
Pixel은 화면을 표현하기 위해 사용하는 가장 작은 요소

Pixel의 모양은 꼭 가로 세로 1:1의 정사각형은 아니다 다른 비율의 Pixel 또한 존재

Pixel에 대한 가로, 세로의 비율을 **픽셀 종횡비(PAR, Pixel Aspect Ratio)**라 함

### 해상도(Ressolution)
화면(Screen)의 Pixel 갯수, Pixel 단위의 가로x세로 형식으로 나타냄

Pixel의 비율(PAR)처럼 해상도 비율도 존재 **DAR(display Aspect Ratio)**, **그림 종횡비(Picture Aspect Ratio)** 또는 **프레임 종횡비(Frame Aspect Ratio)** 라고도 함

Video는 다른 비율을 가진 Pixel을 다양한 화면비를 가진 화면에 그리기 위해 **저장 종횡비(SAR, Storage Aspect Ratio)** 라는 개념을 사용함

**SAR * PAR = DAR**

Example)

PAR = 1.5 : 1, DAR = 16 : 9

SAR = 32:27

### YUV 444
4개의 Pixel에 Y, U, V를 하나씩 사용, RGB와 마찬가지로 하나의 Pixel을 표현하기 위해 Y, U, V를 8bit씩 총 24bit 사용

Y가 4바이트 올때 U도 4바이트 V도 4바이트 온다

![yuv444](https://hankyojeong.github.io/assets/images/mediaBasicKnowledge/yuv444.png)

### YUV 422
4개의 Pixel에 4개의 Y를 사용, 2개의 Pixel 마다 U와 V를 하나씩 사용 => 2개의 Y가 하나의 U와 V값을 참조

하나의 Pixel을 표현하기 위해 16bit가 필요함

![yuv422](https://hankyojeong.github.io/assets/images/mediaBasicKnowledge/yuv422.png)

### YUV 420
4개의 Pixel에 4개의 Y를 사용, 2개의 Y마다 U와 V를 번갈아 가며 사용 => 하나의 Pixel을 표현 하는데 12bit가 필요

![yuv420](https://hankyojeong.github.io/assets/images/mediaBasicKnowledge/yuv420.png)

### 비디오 압축
비디오는 수 많은 프레임(정지 이미지)이 시간 축을 기준으로 모아 저장된 것.

비디오를 압축할 때는 하나의 프레임과 주변 프레임과의 상관관계를 이용해 압축함
이때 기준이 되는 프레임을 I-Frame이라 함. 반대로 상관관계에 있는 프레임은 P-Frame(Predicted Frame)과 B-Frame(Bi-directional)이라 함

P-Frame, B-Frame을 Inter Frame 혹은 Reference Frame이라고도 함

비디오 Frame은 GOP(Group Of Picture)라는 그룹 단위로 압축함
GOP의 범위는 I-Frame과 다음 I-Frame사이로 P-Frame과 B-Frame이 이 그룹안에 존재함

![gop](https://hankyojeong.github.io/assets/images/mediaBasicKnowledge/gop.png)

- I-frame
  - 하나의 온전한 이미지를 저장 => 영상을 Decoding시 다른 Frame은 필요로하지 않음
- P-frame
  - I-frame 이후 다음 I-frame 까지의 변경된 정보만을 가짐
  - P-frame 디코딩시 반드시 P-frame과 연결된 I-frame이 필요
- B-frame
  - P or I-frame과 다음 P-frame의 변경된 정보만을 담고 있음
  - But, 디코딩시 가장 많은 정보(P, I-frame)가 필요
  - B-frame이 많은 영상은 디코딩시 큰 부하를 줄 수 있음


### Audio Sampling
아날로그 신호로 된 소리 데이터를 디지털 장비에서 사용하기 위해서는 Sampling(Analog 신호를 일정 구간을 단위로 표본화하여 저장하는 방식)이라는 과정이 필요

소리를 구간 T로 나누어 표본화

T: Sampling Frequency or Sampling Rate(단위: Hz, kHz)

Ex] T = 44.1kHz(44100Hz) 초당 44,100번 샘플링을 진행

하나의 샘플이 가진 강도를 Digital로 표현하는데 사용하는 비트 수를 **bit-depth** 라 함

Ex] bit-depth = 1, 신호의 강도는 0 혹은 1

bit-depth에 따른 표현 가능한 신호의 강도는 2의 N(N = bit-depth)승과 같음. 많은 bit를 사용할수록 정확한 신호의 강도를 표현하는 것이 가능함

### Bit Rate
Video & Audio를 통해 Encoding 할 때는 Bit rate를 할당하게 됨

Bit Rate란 특정한 시간(보통은 초)단위 마다 처리할 수 있는 비트 수로 인코딩시 Bit rate를 어떻게 할당하느냐에 따라 최종 결과물의 품질이 크게 달라짐

작은 해상도와 낮은 Sampling Rate을 가진 영상을 인코딩시에는 많은 Bit rate가 필요하지 않음

그러나 큰 해상도와 높은 Sampling Rate를 가진 영상을 낮은 Bit Rate 할당하여 인코딩 시에는 화면이 뭉개지고 잡음이 심해짐

Bit Rate 할당 방식
- VBR(Variable BitRate)
- CBR(Constant BitRate)
- ABR(Average BitRate)

### VBR(Variable BitRate)
영상의 복잡동에 따라 할당하는 Bit-Rate의 양이 결정됨

움직임이 많은 구간 -> 압축률이 낮음 -> 높은 bitrate를 할당

움직임이 적은 구간 -> 압축률이 높음 -> 낮은 bitrate를 할당

But, 영상의 복잡도는 인코딩 중 실시간으로 이뤄짐 -> 효율적인 bit rate 할당이 이뤄지지 않음
이러한 문제를 해결하기 위해 **2-pass** 방식을 사용함

- 2-Pass 방식
  - 영상의 복잡도를 먼저 계산 후 이 뎅이터를 기준으로 효율적인 Bit Rate를 할당, 그러나 인코딩시 시간이 기존에 비해 2배로 걸림 (Ex] h.264)

### CBR(Consttant BitRate)
영상의 복잡도와 관계없이 항상 같은 양의 bit-rate를 할당

bit-rate의 양이 일정하여 File의 전체 크기를 미리 가늠 가능, Live Streaming시 필요한 최소 bandwidth를 알 수 있는 장점이 존재

### ABR(Average Bitrate)
영상의 복잡도에 따라 bit-rate를 할당, 그러나 평균으로 지정된 bit-rate를 유지하려 함

VBR처럼 들쑥날쑥한 bit-rate 할당이 이뤄지지 않기에 Streaming에도 무리가 없음, CBR에 비해 높은 품질을 보임