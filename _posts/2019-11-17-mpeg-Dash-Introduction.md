---
title: "Introduction about DASH Streaming protocol"
date: 2019-11-17 12:38:00
categories: media dash streaming
---

# DASH
DASH는 mpeg에서 만든 HTTP를 통해 만든 Streaming을 위한 프로토콜.<br>

## MPD Structure
MPD란 XML 기반의 Media Presentation Description의 약자로 DASH는 MPD구조로 구성.<br>
![mpdStructure](./imageStorage/MPDStructure.png)

* MPD<br>
Media Presentation을 구성하는 시간 순서

* Period<br>
Media content를 사용할 수 있는 미디어 콘텐츠 시간(period)을 나타냄.<br>
기간(period)동안은 변할 수 없습니다.(같은 호환되는 인코딩 버전이 아닙니다)<br>
Ex] Available bitrates, languages, captons, subtitles etc.

* Adaption Set<br>
미디어 콘텐츠 구성 요소의 호환 가능(interchangeable)  인코딩 버전 집합을 나타냄.

* Representation<br>
전달되는 인코드된 버전의 하나 또는 여러개의 Media Content 컴포넌트들.<br>
클라이언트에서는 Network의 상태에 따라서 Representation와 Representation 사이에서 선택할 수 있습니다.

* Sub-Representation<br>
Representation에 내장된 하나 혹은 여러개의 Media Content 컴포넌트들의 특성들(property).<br>
Ex] 
  - Embedded Audio Component -> codec, sampling rate, etc..
  - Embedded subtitle -> codec, etc...

* Segment<br>
HTTP 요청으로 인해 받은 가장 큰 단위의 데이터.

* Sub-Segment<br>
전체 접근 단위들(access unit)에 대한 정보를 가지고 있습니다.<br>
Ex] ISO기반의 미디어 파일 형식에서 SubSegment는 movie fragment들을 항상 가지고 있어야만 합니다.

## Attributes & Elements

### MPD Tag's Attributes & Elements

* id<br>
MPD의 ID

* profile<br>
RFC6381에 따른 URI (ex]urn:mpeg:dash:profile:isoff-on-demand:2011)

* availabilityStartTime<br>
특정 시간 이후부터 해당 컨텐츠에 접근 가능(UTC)<br>
mpd의 type 속성이 dynamic일 경우 무조건 있어야만 하는 속성

* availabilityEndTime<br>
특정 시간까지 해당 컨텐츠에 접근 가능(UTC)

* mediaPresentationDuration<br>
컨텐츠의 전체 시간<br>
mpd의 타입이 static일 경우는 무조건 있어야만 하는 속성(ex]mediaPresentationDuration="PT135.650S")<br>
Check the WIKI : [ISO 8601 - Duration]

* minimumUpdatePeriod<br>
MPD의 update 여부를 확인해야 하는 최소주기

* minBufferTime<br>
몇 초 전의 Media Data까지 버퍼링할 것인지 정의<br>
Representation 태그의 bandwidth 속성을 곱하여 버퍼크기를 결정.

* timeShiftBufferDepth<br>
MPD type 속성이 dynamic일 경우 현재 시간 기준 몇 초 전부터 재생할 것인지를 정의<br>
이 속성이 정의되어 있지 않다면 static일때와 같이 동작

* suggestedPresentationDelay<br>
MPD 타입이 dynamic일 경우 몇 초 뒤부터 해당 유닛에 접근 가능한지(offset)

* maxSegmentDuration<br>
MPD 내부 모든 segment들 중 가장 큰 duration 값

* maxSubSegmentDuration<br>
MPD 내부 모든 Subsegment들 중 가장 큰 duration 값

### Period Tag's Attributes & Elements
* id<br>
Media presentation에서 unique ID

* start<br>
Period의 시작 시간

* duration<br>
Period의 duration<br>
다음 Period의 start는 현재 period의 start + duration.

* bitstreamSwitching<br>
값이 true일 경우 해당 Period의 모든 AdaptionSet의 bitstreamSwitching값은 모두 true



<!--
Reference other site
-->
[ISO 8601 - Duration]: https://en.wikipedia.org/wiki/ISO_8601#Durations