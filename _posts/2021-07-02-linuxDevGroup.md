---
title: "Organization related to Linux Development"
date: 2021-07-02 00:10:00
categories: linux
---

# Linux 개발과 관련된 단체

## CPU 벤더
CPU를 설계하는 회사 (ex] ARM, Intel, IBM)

Linux Kernel의 핵심기능은 CPU에 따라 구현방식이 다르기 때문에 CPU 벤더 또한 Linux Kernel 개발에 참여
(System Call, Exception, Content Switching)

### CPU Architecture와 Linux Driver 계층도
![linuxDriverHierarchy](https://hankyojeong.github.io/assets/images/linux/linuxDriverHierarchy.png)

Linux Kernel은 다양한 CPU Architecture와 함께 구동, Kernel의 핵심동작은 서로 다른 CPU Assembly Code로 구현

## SoC 벤더
SoC (System On Chip), 전자 시스템들의 모든 구성 요소를 통합한 직접 회로
(ex] 브로드 컴 - BCM2837, 삼성 - Exynos, Qualcomm - Snap Dragon)

SoC 벤더는 리눅스 버전을 선택하여 CPU Vendor로 ToolChain을 받아 자신의 SoC Spec에 맞게 Linux Kernel 코드 수정 및 Driver 추가

Linux Kernel을 사용해 SoC HW를 제어하는 Device Driver를 작성 (ex] 엔비디아 SoC와 퀄컴 SoC의 GPU는 자사의 SoC HW에 맞게 설계 되나 서로 다른 Device Driver가 있음)

## 보드 벤더 및 OEM(Origianl Equipment Manufacturer)
SoC가 릴리즈한 Linux Kernel Code를 받아 제품 Spec과 시나리오에 맞게 제품 개발

보드 벤더는 Raspberry PI 재단과 같은 업계이고 OEM은 삼성, LG와 같이 상용제품 개발 업체

SoC에서 제작한 Linux Driver 코드(Linux Kernel + Soc Driver)를 받아 개발