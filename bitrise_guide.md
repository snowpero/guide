# Bitrise 빌드 설정 관련 정리

## Before

- 회사내 MacMini 서버에 Jenkins를 설치해서 사용중
  - Jenkins에 문제가 생길 경우 항상 관리해줘야 함
  - AWS를 이용할 경우 담당자 도움도 필요
  - Android SDK 관리 
- github 연결은 개인 계정으로 되어 있음

## Todo

- github는 회사 계정으로 설정할 것
  - 개인 계정의 경우 퇴사할 경우 문제
- Jenkins 설정에 많은 시간이 소요되며, 향후 관리도 꾸준히 해줘야하는 단점을 보완
- 설정이 간편
- Bitrise 서비스 선택
  - Free Plan
    - 2 team members
    - 200 builds / month
  - Developer Plan
    - 36달러 / month
  - 무료 플랜으로도 충분히 가능하다고 생각
  - 빌드 서버 관리 불필요
  - slack과 email 연동
    - email 연동은 기본
    - 나머지 배포 서비스나 Slack 연동은 옵션



## Setting

1. https://www.bitrise.io/ 접속 후 계정 생성
2. Account Setting에서 github 계정 연결
3. Dashboard - Add New App
   - github에서 repository 선택
   - ssh 생성해서 private key 따로 저장 후 설정
4. Workflow Editor
   - 안드로이드 빌드 옵션 추가
     - https://medium.com/@AndreSand/building-the-android-debug-app-flavorwith-bitrise-7825e481a50a
   - Slack Message 추가
     - Slack webhook 생성
       - https://api.slack.com/messaging/webhooks
       - Imcoming Webhooks 메뉴에서 Webhook URL 찾아서 입력
     - Slack Message 설정 가이드 : https://blog.bitrise.io/slack-away
5. bitrise.yml 파일 수정
   - Slack Message 설정이 Workflow Editor 내에서 제대로 설정이 안됨
   - 고로 yml 파일을 직접 수정
   - 특히나 webhook url 입력의 경우 바로 yml 파일에 하는 것이 빠름
     - https://qiita.com/a_jike/items/2907ede75f96d123861e
   - Slack Message Format 설정
     - https://qiita.com/a_jike/items/2907ede75f96d123861e
     - bitrise github 샘플 : https://github.com/bitrise-steplib



## Bitrise

접속 : https://www.bitrise.io/

