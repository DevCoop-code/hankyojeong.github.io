---
title: "H264 Stream Format(AnnexB, AVCC)"
date: 2020-09-22 06:30:00
categories: mediaParser
---
# AnnexB & AVCC Format
h264로 인코딩된 비디오는 여러가지 포맷을 가지는데 그 중 대표적인 포맷이 바로 **AnnexB** 포맷과 **AVCC** 포맷. <br>

## NALU(Network Abstraction Layer Unit)
h264 데이터 스트림은 여러개의 NALU(Network Abstraction Layer Unit)들로 구성되어짐
<br>

NALU type은 19개의 서로 다른 타입들이 존재하고 각 타입들은 **VCL**, **non-VCL**로 카테고리화됨
- VCL(Video Coding Layer): VCL 타입은 실제 visual information을 가지고 있는 NALU 
- non-VCL: non-VCL 타입은 실제 정보를 가지고 있는것이 아닌 metadata를 가지고 있는 NALU

아래 그림은 19개의 서로 다른 타입들을 보여줌

![nalu_types](https://hankyojeong.github.io/assets/images/h264StreamFormats/naluTypes.png)

### NALU type들 중 몇몇 주요하게 많이 쓰이는 NALU type들
1. SPS(Sequence Parameter Set)
   - non-VCL NALU
   - Decoder를 구성하는데 필요한 정보들을 가지고 있음(ex] profile, level, resolution, frame rate, ...)
2. PPS(Picture Parameter Set)
   - non-VCL NALU
   - entropy coding mode, slice groups, maaster prediction & deblocking filter 등을 가지고 있음
3. IDR(Instantaneous Decoder Refresh)
   - VCL NALU
   - self contained image slice
   - 다른 NALU들을 참고하지 않더라도 디코딩하고 화면에 뿌려질수 있음
4. AUD(Access Unit Delimiter)
   - Optional NALU
   - 프레임을 기본 스트림으로 구분하는데 사용


## AnnexB
첫 시작을 3bytes(0x00 00 01) 혹은 4bytes(0x00 00 00 01)의 Header로 시작, 이를 기준으로 NALU를 분리함 <br>
header 이후 1바이트를 통해 NALU의 type을 알 수 있음
- SPS: 00 00 00 01 **67**
- PPS: 00 00 00 01 **68**
- IDR: 00 00 00 01 **65**
- non-IDR: 00 00 00 01 **61**

보통 SPS, PPS NALU로 시작하고 그 후 IDR, non-IDR NALU가 반복됨
## AVCC
각각의 NALU는 자신의 사이즈 정보를 헤더로 앞에 둠(Big Endian Format) <br>
사이즈 정보가 앞에 있어 파싱은 쉽지만 AnnexB의 Byte Alignment 특징을 잃음 


## Reference
https://stackoverflow.com/questions/24884827/possible-locations-for-sequence-picture-parameter-sets-for-h-264-stream