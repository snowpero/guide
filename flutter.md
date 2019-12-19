## Flutter 관련 정리

#### firebase_auth

* iOS / Android에 따라 지원하는 버전이 다름

  * https://pub.dev/packages/firebase_auth/versions

  * Stable 버전을 참고해서 두 플랫폼다 호환되는 버전 확인
  * iOS에 맞추고 Android에서 Gradle 설정을 바꾸는게 빠름

#### 빌드 명령어

* Android
  * flutter build apk --flavor production --target "lib/**.dart" --target-platform=android-arm64(64비트 지원 필수 옵션)
* iOS
  * Flutter build iOS "lib/**.dart"
* 빌드 후 각 플랫폼에 맞게 스토어 배포

#### pubspec.yaml

* 앱 버전과 3rd Party 라이브러리 버전 지정 : gradle 의 형태와 매우 유사
* 스토어key의 경우 안드로이드 key.properties 에서 설정

#### 이슈 사항

* firebase의 경우 iOS 에서 product / staging 과 같이 json 파일을 나눠 확인 불가능



