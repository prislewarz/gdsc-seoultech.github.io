---
layout: post
title: Candiformation 10주차 보고서
date: 2022-03-15
author: Yangyongsu
description: "candiformation 10주차 보고서!!"
categories: ["1st_term"]
tags: ["solution_challenge", "candiformation"]
---

# Candiformation 대선이 끝난 뒤...우리는?

## 제20대 대통령 선거날: 3월 9일
제20대 대통령 선거가 끝났습니다.  
구글 플레이스토어에 업로드 한 3월 1일 이후 여러가지를 수정하고 리팩토링을 했지만   
아래의 여러가지의 이유로 플레이스토어에서 리젝을 당했습니다. 

v1: 리젝  
v2: 앱 설명 수정 → 업로드 / 구글로그인 안됨, 정당정보화면 미완성  
v3: 정당정보화면 못가게 막음 / 구글로그인 고쳤으나 안됨  
v1.0.4: 구글로그인 고쳐서 재배포 (되는지 모름) + 닉네임유효성검사, 앱공유기능  
v1.0.5: 설명수정 → 리젝 / 사유: 유저가 자기 정보가 어떻게 활용 되는지 알수가 없다~  
v1.1.0: 이메일/닉네임 중복체크, 서비스이용약관/개인정보처리방침 추가  

## 그래도…

그래도 플레이스토어에 올렸다는 것으로 의욕이 많이들 빠지긴 했지만   
프로젝트의 완성도를 위해서 하나하나 리펙토링 요소를 정리하고 중요도를 나눠 완성도를 높이기로 결정했습니다.   

## 1. 리펙토링 요소 중요도 나누기와 체크리스트


**안드로이드**

* [x] 기종에 따라 맨 오른쪽 카드가 작게 보임(후보자 화면)
* [x] 박근혜 가족 추가(후보자 화면)
* [x] 댓글 삭제 시 다이얼로그 띄우기
* [ ] 카드 누르면 1이 튀어나옴(후보자 화면)
* [x] navBackStack 제대로 작동 안함(같은화면에서 뒤로가기가 여러번 눌림) → 수정하기
* [ ] 스크린 클래스 만들기 + 바텀바, 네비게이션과 함께 적용
* [ ] 정당정보 화면 추가
* [x] 회원가입 시 이메일 중복체크, 닉네임 중복체크 (api 수정 후)
* [ ] 유저 로그인 상태 정보 어떻게 저장할지 (현재는 currentUser=”” 이런방식) (api 수정 후)
* [ ] response를 클래스에 담아서 로딩화면 + 서버 끊김 화면 등 다양한 화면 보여주기 (현재는 서버 닫히면 앱이 꺼짐) (Resource Wrapper sealed class) (api 수정 후)
* [ ] 회원가입 했을 때 바로 로그인되기 (api 수정 후)
* [x] 비밀번호 유효성 검사
* [x] 뉴스기사 뷰 - 클릭 시 해당 link로 이동(article 페이지x)(홈화면)
* [ ] 뉴스기사 뷰 - 자동으로 넘어가기(시도는 해보겠음)(홈화면)
* [ ] 스낵바 함수화, 위치조정 → 안되면 토스트바 커스텀
* [x] 플레이스토어 등록 완료 시 어플리케이션 공유기능 활성화 (프로필화면)
* [x] 본인이 쓴 댓글 화면에서 지울 수 있는 기능 추가
* [x] OAuth 현재방식 : sdk로 구글로그인 → 이메일, 닉네임 정보 받아오기 → 서버에 전달. 이 방식이 맞는가? (맞는 것 같음, 틀리면 어쩔? 돌아가는데)
* [ ] 백엔드와 회의를 해서 필요없는 api에 request나 response가 있는지, 통합할 부분이나 아낼 부분이 있는지 등 수정하기
* [ ] 하트, 댓글 아이콘이랑 옆에 숫자랑 라인이 달라보임(같도록 코드짜긴 함) (기사화면)
* [x] 뉴스 언론사 기울임체 별로란 피드백이 있습니다. (기사화면)
* [x] 기사 공유아이콘 및 기능 추가    → 링크 복사 기능으로 수정
* [x] 뷰모델 필요없는 로직, 중복 로직 정리 (api 수정 후)

**백엔드**

* [ ] JWT → refreshToken
* [ ] Oauth
* [ ] 과연 ResponseEntity로 return 하는 게 맞는건가 자꾸 httpStatus가 중복
* [ ]  * [ ] success and Failure response도 없애기
* [x] 회원가입 api 중복체크 짜주기 먼저 이메일 중복, 닉네임 중복
* [x] 그리고 지금 서버가 한 개인데 만일 서버에 다시 올리면 이게 잠시 멈추는데 이럴땐 어떻게 해야되는건가!
* [x] redis 써보기 → 시간에 따라서 달라지는 자료에 적합(refreshToken, email Code)
* [ ] api 문서화
* [ ] 백엔드와 회의를 해서 필요없는 api에 request나 response가 있는지, 통합할 부분이나 깎아낼 부분이 있는지 등 수정하기
* [x] github 이력 지우기(1순위)
* [x] 아 python 크롤링 자동화 다시 해야됨
* [ ] Entity에 setter 없애고 대체할 방법 찾기
* [ ] 조금 더 객체지향적인 방법으로 코딩해보기
* [ ] 생성자 주입할 때 field 주입말고 생성자 주입으로
* [ ] clean코드 적용, 불필요한 주석 다 없애기, 함수명도
* [ ] DB table명 바꿔야되고,, 몇 개 class 이름도 바꿔야됨
* [ ] 무지성 final 삭제
* [ ] travis 해보기
* [ ] IP를 어떻게 해야되나!
* [ ] 로드밸런서도 해보기
* [ ] service도 interface 만들어서 SOLID 만족하게..
* [ ] 테스트 코드를 작성,,,해...볼..까요..?


이렇게 체크리스트를 만들어 리펙토링을 하고 있습니다.  

## 현재 상황

아직까지도 리젝인 상황이고, 앞으로 준비해야할 것들은 솔루션 챌린지 마지막 요소들로 많은 노력을 기울일 것입니다.  
앞으로도 우리 Candiformation은 계속됩니다!

* 리드미 
* 동영상
