---
title: "Bounds vs Frame"
date: 2020-09-22 06:30:00
categories: iOS
---

# Bounds vs Frame
Bounds: 뷰의 위치가 뷰 자신의 좌표계에 의해 결정 <br>
Frame: 뷰의 위치가 부모 뷰에 의해 결정

![FrameVSBound](https://hankyojeong.github.io/assets/images/iOS/Frame-Bound.png)

Frame은 단순히 만드려는 뷰를 나타내는것이 아닌 만드려는 뷰를 감싸는 사각형 모양의 뷰, Frame의 좌표와 크기도 이렇게 감싸는 사각형의 좌표와 크기를 나타냄

![FrameVSBound2](https://hankyojeong.github.io/assets/images/iOS/Frame-Bound2.png)


Frame은 감싸고 있는 뷰가 회전한다면 그에 맞춰 크기와 좌표가 바뀌게 됨. 그러나 Bounds는 좌표와 크기가 유지됨

Frame은 좌표를 기준으로 움직이는 Animation에 사용되기 적합하고 Bounds는 회전된 뷰의 Width, Height를 알기에 적합함