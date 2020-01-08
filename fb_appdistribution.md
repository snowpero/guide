## Firebase AppDistribution + Gradle



#### 준비단계

* Fabric 서비스의 종료로 인해 Firebase로의 이전이 필요
* Fabric Beta 서비스와 거의 동일
* App 배포 서비스들을 알아보던중 무료로 잘 관리되는 AppDistribution 선택

#### 관련 자료 링크

* https://firebase.google.com/docs/app-distribution/android/distribute-gradle?hl=ko
  * 공식자료가 너무 잘나와있어 따로 설정에 대한 설명은 링크로 대체
* https://blog.codemagic.io/firebase-app-distribution-with-codemagic/

#### 이슈 사항

* Firebase json을 빌드마다 따로 관리하고 있다면, 토큰도 따로 관리해야함



#### Gradle 

* 옵션값으로 releaseNotesFile 설정을 통해 배포시 ReleaseNote 설정 가능
* ![device-2020-01-08-144817](/Users/gilyongpark/Documents/img_edit/device-2020-01-08-144817.png)

* ReleaseNote 쓰기
  * 수동으로 ReleaseNote를 작성하지 않고 빌드시 자동으로 작성이 되도록 구현
  * Gradle 내 사용중인 App 정보 + Git Commit 으로 ReleaseNote 구성
  * Git Commit 정보 가져오기
    * org.ajoberstar:grgit 라이브러리 사용 : https://github.com/ajoberstar/grgit
    * 해당 라이브러리를 통해 Branch, Commit 한 계정, Commit Message 추가

`

```Gradle
task writeReleaseNote() {
    println '[writeReleaseNote Start]'

    def gitBranchName = git.branch.current().name.replaceAll(/(.*)\//, '')
    def committer = grgit.head().committer
    def message = grgit.head().shortMessage

    def verCode = getVersionCodeTimestamp()
    def verName = rootProject.ext.versionName

    new File(projectDir, "release_notes.txt").text =
            """
Buildtime: ${new SimpleDateFormat("yyyy년 MM월 dd일 E요일 HH:mm:ss", Locale.KOREAN).format(new Date())}
VersionCode : $verCode
VersionName : $verName
BranchName : $gitBranchName
Committer : $committer
Message: $message
"""
}
```

`

#### 보완 또는 추가 개발(또는 설정) 해야 할 점

* 로컬 Build를 이용하므로, CI를 이용하여 자동빌드 적용 : Jenkins 또는 AWS CodeBuild
* 빌드 서버를 별도로 구성하여, 일정한 결과가 나오도록 유지
* Firebase Token 값 때문에 쉘스크립트 파일(.sh)을 이용해 빌드
  * Firebase 인증을 Google Cloud Platform 을 이용해서 관리해야 할듯 : token 값이 없는 json 키 사용
