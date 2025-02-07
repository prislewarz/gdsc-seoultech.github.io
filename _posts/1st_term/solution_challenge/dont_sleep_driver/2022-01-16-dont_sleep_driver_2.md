---
layout: post
title: <dont_sleep_driver> 3주차 이야기 아이디어 변경!!
date: 2022-01-16
author: InHyeok-J
categories: ["1st_term"]
tags: ["solution_challenge", "dont_sleep_driver"]
---

안녕하세여 new law bot이었다가 아이디어를 변경해서 don't sleep driver로 팀명을 바꿨습니다!

## 아이디어를 바꾼 이유

기존의 핵심 기능, 정치인의 발의 내용 조회 및 법 조회가 이미 앱스토어에 등록된 앱들이 많았습니다.  
법 -> 법제처에서 만든 앱,  
정치인 -> 정치IN

법과 관련한 기능은 법저체에서 제공하는 기능보다 퀄리티있게 못할 것 같았고, 정치IN에서 제공하는 정치인의 발의 내용 조회등은 저희가 구상했던 아이디어와 동일했습니다.  
저희는 배포를 고려해서 아이디를 생각중이었기 때문에 아이디어가 겹치는것을 최대한 피하려고해서 이번에 새롭게 기획을 했습니다.

# Don't Sleep Driver

일단! 솔루션 챌린지때 구현할 앱인 Don't Sleep Driver 입니다.  
핵심 기능은 카메라로 얼굴 인식을 통해, 사용자가 졸고 있는지를 확인해서 알림을 보내는 기능인데요  
이름 그대로 `Don't Sleep Driver` 입니다 ㅎㅎ

여기서 `일단?` 이라고 한것은 배포용으로 기획을 한다고 했는데 이 얼굴인식을 통한 졸고있는지 확인하는 기능을 핵심 기능으로 가지고 , 추 후 공부용 앱으로 공부에 집중하기 위한 앱을 만들려고 합니다. 즉 솔루션 챌린지 전용 앱과 배포용 앱 두가지를 구현하려고 생각중이에요!

일단 교육용앱은 나중에 기회가 있다면 알려드리고 Don't Sleep Driver의 기능을 소개해드리겠습니다.

## 핵심 기능

1. 유저 회원가입 및 로그인
2. 운전 시작! 버튼을 누르면 카메라가 켜지면서 분석시작
    1. 동시에 안드로이드 GPS 데이터 받아옴
    2. 카메라 인식을 할 수 없으면?
        1. 얼굴이 없는경우
            1. 화면 view 얼굴이없다고 그려주고
        2. 각도가 이상한 경우
            1. 각도가 이상하다고 view에 그려주고
        3. 카메라 화질이 안되는 경우 **( 야간 분석은 ? )**
            1. 고려안함
    3. 운전중에 계속 분석 하다가 특정 기준이 된다면 졸음운전이라고 판단해서 알림
    4. 종료버튼
    5. 안드로이드는 백엔드 서버로 데이터 전송
3. 사용자는 자신의 운전 기록을 Map api 함께 확인 가능
    1. 졸음 경고 횟수
    2. 추후 개발( 졸음 레벨을 세분화해서 분석)
    3. 경고 및 통계는 시각화 가능?
4. 알림 소리 변경

저희의 기능은 많지 않고 딱 핵심 기능 위주로 구현 예정입니다.  
얼굴 인식과, 알림 보내기, gps 데이터 받아오기 3가지 기능을 바탕으로 운전자가 졸고 있느지 분석해서 알림을 보내주고, 추 후에 기록을 남겨서 자신의 운전 기록을 지도로 확인 가능하며 어느 운전 구간때 졸고 혹은 위험했는지 알려줍니다!

## 아키텍처

<img src="https://user-images.githubusercontent.com/28949213/149775978-f3b02e46-86f3-4c64-b1a6-637b433ad18b.png">

진짜 간단하게 그린 아키텍처입니다.
안드로이드 내장 ML kit을 이용한 얼굴 분석 및 데이터를 가져오고, 안드로이드 안에 TensorFlow 를 내장해서 분석 후 졸음 상황때 알림을 보냅니다.

ML부분을 내장시킨 이후는 최대한 네트워크 전송 과정을 최소화하기 위해서인데요 , 그래서 운전 종료시에 데이터를 한번에 백엔드 서버로 보내서 DB에 저장시킬 예정입니다.

하지만 이 아키텍처는 졸음 분석 모델이 지속적으로 학습이 안된다고 하는데요(?)아마도...
그래서 추후 발전 방향으로 영상 이미지 데이터를 보내 ML로 새로 학습시키고, 릴리즈 버전때마다 모델을 업데이트 시키는 방향 or 실시간으로 학습 시켜서 좀더 정확도 있는 졸음 인식을 할 수 있게 하는 방향 2가지로 추후에 발전시킬 예정입니다.

현 상황은 백엔드 개발자가 할일이 거의 없네요.. 만약 추후 발전 단계가 된다면 ML 개발자와 함께 MLOps를 구축해볼 생각에 설레네요 !
