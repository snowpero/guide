# AWS Android 빌드

### 사전 준비

* AWS 계정 관련 설정
  * 진행중 AWS 관련 계정 권한 문제가 생길 수 있으니, 권한 부여 관련 설정법 숙지
  * 계정 로그인 후 지역 설정
    * CodeBuild 가격표 비교해보면 서울 지역으로 설정해야 빌드 비용이 가장 저렴
* 단점
  * S3까지 APK 파일을 옮긴 후 public으로 배포하기 어려움

### CodeBuild

* 빌드 프로젝트 생성
  * 프로젝트 구성 - 알아보기 쉬운 이름으로 정의
  * 소스
    * github : Personal access token 사용
    * 레파지토리 선택
  * 환경
    * 관련 설명 링크 : https://docs.aws.amazon.com/ko_kr/codebuild/latest/userguide/sample-runtime-versions.html
    * 운영 체제 : Amazon Linux 2
    * 런타임 : Standard
    * 이미지 :  x86_64-standard:1.0
    * 나머지 기본값
    * 추가구성
      * 제한시간 : 빌드시 제한시간이 넘어갈 경우 빌드 중단하는 옵션. 15분정도 설정
      * 컴퓨팅
        * 사양에 따라 요금차이
        * 요금 관련 정보 링크 : https://aws.amazon.com/ko/codebuild/pricing/
        * 3GB 메모리, vCPU 2개(0.005달러) vs 7GB 메모리, vCPU 4개(0.01달러)
        * 0.045 ~ 0.05달러(10분 내외) vs 0.05~0.06달러(5~6분내외)
        * 요금 0.01달러 정도 차이
        * 속도 빠른 7GB, vCPU 4개짜리 선택
    * BuildSpec
      * buildspec.yml 파일 생성 후 commit
      * staging, release 등 용도에 맞게 파일 따로 생성 후 buildspec 설정에서 파일명 지정
      * 관련 링크 1 : https://docs.aws.amazon.com/ko_kr/codepipeline/latest/userguide/tutorials-codebuild-devicefarm.html
      * 관련 링크 2 : https://medium.com/@SungMinLee/aws-codebuild-codecov-%EB%A1%9C-%EC%A0%80%EB%A0%B4%ED%95%98%EA%B2%8C-android-ci-%EA%B5%AC%EC%B6%95%ED%95%98%EA%B8%B0-2a209651c4f7
      * 주의 사항
        * AWS 에서 버킷(S3) 생성 및 권한 필요
        * apk 경로 아티팩트는 buildspec 파일에서 설정
          * artifacts - files 관련 설명
            * S3 로 업로드할 대상 지정
            * 관련 링크 : https://jojoldu.tistory.com/283
    * Webhook
      * CodeBuild - 소스 편집에서 Webhook 이벤트 설정 가능
    * 아티팩트
      * 관련 링크 : https://aws.amazon.com/ko/blogs/mobile/automatically-build-your-android-app-with-aws-codebuild/
      * S3 로 설정
        * AWS 에서 버킷 생성 및 권한 필요
        * 이름 : 구분 폴더명
        * 빌드 후 APK 파일 경로는 buildspec.yml에서 설정
