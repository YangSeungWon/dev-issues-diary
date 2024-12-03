---
layout: post
title:  "Sorry, your sign-in attempt doesn't match the Egress IPs of the profile that this machine is assigned to. Please contact your IT administrator"
date:   2024-12-03 15:30:00 +0900
tags: adobe
---

Sorry, your sign-in attempt doesn't match the Egress IPs of the profile that this machine is assigned to. Please contact your IT administrator 문제 해결.

# 문제 상황
웹에서 어도비 계정을 접속해보면 기관 등록이 제대로 된 것이 확인되는데, 컴퓨터에 설치된 creative cloud나 adobe 프로그램들에서는 확인할 수 없다고 뜨고, 프로그램을 열면 로딩 후 `Sorry, your sign-in attempt doesn't match the Egress IPs of the profile that this machine is assigned to. Please contact your IT administrator` 라고 뜨며 강제 종료된다. 한글로는 로그인 시도가 이그레스 IP와 일치하지 않습니다. 관리자에게 문의해주십시오. 정도의 메시지가 떴었다.

# 해결 방법

[출처](https://community.adobe.com/t5/enterprise-teams-discussions/help-needed-egress-ip-s-not-recognized/td-p/10439208?profile.language=en)

```bash
sudo rm -rf "/Library/Application Support/Adobe/OperatingConfigs"
```
