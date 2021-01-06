---
title: "FFMpeg APIs"
date: 2021-01-05 09:43:00
categories: ffmpeg
---

# FFMpeg APIs
ffmpeg 라이브러리를 사용하기 위한 기본 API 소개

### APIs
- av_register_all
- avformat_open_input
- avformat_find_stream_info
- av_read_frame
- av_free_packet

### AVPacket, AVFrame
- AVPacket
  - Codec으로 압축된 스트림 데이터를 저장
- AVFrame
  - Decoding한 압축되지 않은 RAW 데이터를 저장
  - 비디오의 해상도, Sample Rate, Channel 정보와 같은 정보를 얻어올수 있음

### ffmpeg API Flow
1. **av_register_all** : Register the ffmpeg lib
2. **avformat_open_input** : Media File 열기(Open an input stream)
3. **avformat_find_stream_info** : Stream 정보 가져오기(Read packets of a media file to get stream information)
4. **avcodec_find_decoder** : 해당 미디어의 Codec 찾기
5. **avcodec_open2** : 찾은 AVCodec을 이용해 AVCodecContext를 초기화
6. **av_read_frame** : Stream의 다음 Frame을 읽음
7. **av_packet_rescale_ts** : Packet 안의 Timestamp, Duration 값을 유효한 Time Field로 바꿈
8. **avcodec_decode_video2**, **avcodec_decode_audio4** : Decoding
9. **av_frame_get_best_effort_timestamp** : AVPacket에 있는 PTS와 DTS를 자동으로 AVFrame과 동기화 하기 위해 사용함
