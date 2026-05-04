# Deploy Guide

## 프로젝트명
AI 감정일기 (Emotion Diary)

## 작성일
2026-05-04

---

## 배포 구조
GitHub Push
↓
GitHub Actions (자동 실행)
↓
Flutter Test → Flutter Build
↓
Firebase App Distribution
↓
테스터 기기에 앱 배포

---

## 1. Firebase 프로젝트 설정

### Firebase 프로젝트 생성

https://console.firebase.google.com 접속
[프로젝트 추가] 클릭
프로젝트 이름: emotion-diary
[계속] → [프로젝트 만들기]


### iOS 앱 등록

Firebase 콘솔 → [앱 추가] → iOS 선택
Bundle ID 입력: com.ichaeyeon.emotiondiary
GoogleService-Info.plist 다운로드
app/ios/Runner/ 폴더에 파일 이동


---

## 2. Firebase App Distribution 설정
Firebase 콘솔
→ [App Distribution] 메뉴
→ [시작하기] 클릭
→ 테스터 이메일 추가

---

## 3. GitHub Secrets 설정

GitHub Actions에서 사용할 비밀 값 등록:
GitHub 리포지토리
→ [Settings] → [Secrets and variables] → [Actions]
→ [New repository secret]

등록할 Secrets:

| 이름 | 값 |
|---|---|
| `CLAUDE_API_KEY` | Anthropic API Key |
| `FIREBASE_APP_ID` | Firebase 앱 ID |
| `FIREBASE_TOKEN` | Firebase CI 토큰 |

### Firebase 토큰 발급
```bash
npm install -g firebase-tools
firebase login:ci
# 출력된 토큰을 FIREBASE_TOKEN으로 등록
```

---

## 4. GitHub Actions 워크플로우 설정

`.github/workflows/deploy.yml` 파일 생성:

```bash
mkdir -p .github/workflows
touch .github/workflows/deploy.yml
```

아래 내용 붙여넣기:

```yaml
name: Flutter CI/CD

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    name: Test
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v4

      - name: Flutter 설치
        uses: subosito/flutter-action@v2
        with:
          flutter-version: '3.x'
          channel: 'stable'

      - name: 패키지 설치
        run: |
          cd app
          flutter pub get

      - name: 테스트 실행
        run: |
          cd app
          flutter test

  build:
    name: Build & Deploy
    runs-on: macos-latest
    needs: test
    if: github.ref == 'refs/heads/main'
    steps:
      - uses: actions/checkout@v4

      - name: Flutter 설치
        uses: subosito/flutter-action@v2
        with:
          flutter-version: '3.x'
          channel: 'stable'

      - name: 환경변수 설정
        run: |
          echo "CLAUDE_API_KEY=${{ secrets.CLAUDE_API_KEY }}" > app/.env

      - name: 패키지 설치
        run: |
          cd app
          flutter pub get

      - name: iOS 빌드
        run: |
          cd app
          flutter build ios --release --no-codesign

      - name: Firebase 배포
        uses: wzieba/Firebase-Distribution-Github-Action@v1
        with:
          appId: ${{ secrets.FIREBASE_APP_ID }}
          token: ${{ secrets.FIREBASE_TOKEN }}
          groups: testers
          file: app/build/ios/iphoneos/Runner.app
```

---

## 5. 수동 배포 (로컬에서)

### iOS 빌드
```bash
cd app
flutter build ios --release --no-codesign
```

### APK 빌드 (Android)
```bash
cd app
flutter build apk --release
# 결과물: app/build/app/outputs/flutter-apk/app-release.apk
```

---

## 6. 배포 확인
Firebase 콘솔
→ [App Distribution]
→ 최신 빌드 업로드 확인
→ 테스터에게 초대 메일 발송 확인

---

## 브랜치 전략

| 브랜치 | 용도 |
|---|---|
| `main` | 배포용 — push 시 자동 빌드 |
| `develop` | 개발용 — 기능 통합 |
| `feature/*` | 기능별 개발 브랜치 |

---

## 자주 발생하는 오류

### CocoaPods 오류
```bash
cd app/ios
pod install --repo-update
```

### 빌드 캐시 오류
```bash
cd app
flutter clean
flutter pub get
flutter build ios
```

---

## 관련 문서
- [setup.md](setup.md)
- [testing.md](testing.md)
- [architecture.md](architecture.md)