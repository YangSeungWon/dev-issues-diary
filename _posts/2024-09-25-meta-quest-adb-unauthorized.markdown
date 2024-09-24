---
layout: single
author_profile: true
title:  "메타 퀘스트 기기가 ADB에서 unauthorized 상태일 때"
date:   2024-09-25 01:30:00 +0900
tags: meta-quest adb
---

메타 퀘스트 기기를 컴퓨터와 USB 케이블로 연결하였을 때, ADB 또는 Meta Quest Developer Hub에서 메타 퀘스트 기기가 인식되지만 'unauthorized' 상태로 표시될 때의 해결 방법입니다.

# 문제 상황

ADB 또는 Meta Quest Developer Hub (MQDH)에서 메타 퀘스트 기기가 인식되지만 'unauthorized' 상태로 표시됩니다.
MQDH에서 말하는대로 메타 퀘스트 기기에서 허용 알림을 눌러도 해결되지 않습니다.

<p align="center">
  <img src="/assets/images/2024-09-25-meta-quest-adb-unauthorized/adb-devices.png" alt="ADB Devices 결과">
  <br>
  <em>그림 1: ADB Devices 결과: unauthorized</em>
</p>

<p align="center">
  <img src="/assets/images/2024-09-25-meta-quest-adb-unauthorized/mqdh.png" alt="Meta Quest Developer Hub 화면">
  <br>
  <em>그림 2: Meta Quest Developer Hub 화면: unauthorized</em>
</p>

# 해결 방법

다음 단계를 따라 문제를 해결할 수 있습니다:

1. 메타 퀘스트 기기에서 USB 케이블을 분리합니다.
2. 메타 호라이즌(Meta Horizon) 앱에서 개발자 모드를 비활성화합니다.
3. 메타 퀘스트 기기를 재시작합니다.
4. 재부팅 후 다시 개발자 모드를 활성화합니다.
5. USB 케이블을 연결하고 헤드셋 내에서 권한 요청을 승인합니다.

출처: [Reddit](https://www.reddit.com/r/sidequest/comments/pkieng/im_seeing_unauthorized_allow_in_headset_and_cant/)

## (번외) 아예 기기가 인식되지 않는 경우

1. [Oculus 개발자 계정 인증 페이지](https://developer.oculus.com/manage/verify/)에서 계정이 3가지 모두 인증되었는지 확인합니다.
2. Meta Horizon 앱에 해당 기기가 등록되어 있고 개발자 모드가 활성화되어 있는지 확인합니다.
3. 메타 퀘스트 기기 알림으로 오는 권한 요청을 승인합니다.
4. (검증 안됨) 메타 퀘스트 기기에 로그인된 계정이 주 계정(primary account)인지 확인합니다.
