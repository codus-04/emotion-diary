# emotion-diary
# 🧠 AI 감정일기 (Emotion Diary)

> 매일 감정을 기록하면 AI가 패턴을 분석해 자기이해를 돕는 모바일 앱

---

## 📱 주요 기능

| 기능 | 설명 |
|---|---|
| 📝 일기 작성 | 텍스트 또는 음성으로 감정 일기 작성 |
| 🤖 AI 감정 분석 | Claude API가 일기 내용의 감정을 자동 분석 및 태깅 |
| 📊 감정 그래프 | 주간/월간 감정 흐름을 시각화 |
| 💡 감정 인사이트 | 나만의 감정 패턴 발견 및 리포트 제공 |
| 🔔 리마인더 알림 | 매일 정해진 시간에 기록 알림 |

---

## 🛠 기술 스택

| 분류 | 기술 |
|---|---|
| 모바일 프레임워크 | Flutter 3.x |
| AI 감정 분석 | Claude API (claude-haiku-4-5) |
| 로컬 DB | Isar |
| 상태 관리 | Riverpod |
| 감정 시각화 | fl_chart |
| 백엔드 | Supabase |
| CI/CD | GitHub Actions + Firebase App Distribution |

---

## 📁 프로젝트 구조
emotion-diary/
├── app/                          # Flutter 앱
│   ├── lib/
│   │   ├── core/                 # 공통 유틸, 상수, 테마
│   │   ├── data/                 # API 호출, 로컬 DB
│   │   ├── domain/               # 비즈니스 로직
│   │   └── presentation/         # UI 레이어
│   ├── test/                     # 단위 + 위젯 테스트
│   └── integration_test/         # 통합 테스트
├── .planning/                    # 기획 문서
│   ├── 00-vision.md
│   ├── 01-requirements.md
│   ├── 02-wbs.md
│   ├── 04-schedule.md
│   └── decisions/                # ADR 문서
│       ├── ADR-001-플랫폼선택.md
│       ├── ADR-002-AI모델선택.md
│       └── ADR-003-감정분석방식.md
├── docs/                         # 기술 문서
│   ├── architecture.md
│   ├── setup.md
│   ├── deploy.md
│   └── testing.md
├── AGENTS.md                     # AI Agent 활용 방식
└── AUTHORING.ichaeyeon.md        # 나만의 AI 협업 방식

---

## 🚀 시작하기

### 사전 요구사항
- Flutter 3.x 이상
- Xcode 15 이상 (Mac)
- Claude API Key ([발급받기](https://console.anthropic.com))

### 설치 및 실행

```bash
# 1. 리포지토리 클론
git clone https://github.com/ichaeyeon/emotion-diary.git
cd emotion-diary

# 2. Flutter 패키지 설치
cd app
flutter pub get

# 3. 환경변수 설정
cp .env.example .env
# .env 파일에 Claude API Key 입력

# 4. 앱 실행
flutter run
```

자세한 설치 방법은 [docs/setup.md](docs/setup.md) 참고

---

## 🧪 테스트 실행

```bash
cd app

# 전체 테스트
flutter test

# 통합 테스트
flutter test integration_test/app_test.dart
```

자세한 테스트 방법은 [docs/testing.md](docs/testing.md) 참고

---

## 📦 배포

```bash
# iOS 빌드
flutter build ios --release --no-codesign

# APK 빌드
flutter build apk --release
```

자세한 배포 방법은 [docs/deploy.md](docs/deploy.md) 참고

---

## 📄 문서

| 문서 | 설명 |
|---|---|
| [비전](./planning/00-vision.md) | 프로젝트 목적 및 방향 |
| [요구사항](./planning/01-requirements.md) | MoSCoW 요구사항 정의 |
| [WBS](./planning/02-wbs.md) | 전체 태스크 분해 |
| [일정](./planning/04-schedule.md) | 6주 개발 일정 |
| [아키텍처](./docs/architecture.md) | 시스템 구조 설계 |
| [ADR-001](./planning/decisions/ADR-001-플랫폼선택.md) | 플랫폼 선택 근거 |
| [ADR-002](./planning/decisions/ADR-002-AI모델선택.md) | AI 모델 선택 근거 |
| [ADR-003](./planning/decisions/ADR-003-감정분석방식.md) | 감정 분석 방식 선택 근거 |

---

## 🤖 AI Agent 활용

이 프로젝트는 Claude AI를 활용해 개발되었습니다.
AI 활용 방식은 [AGENTS.md](AGENTS.md) 참고

---

## 👤 개발자

- **ichaeyeon**
- AI 협업 방식: [AUTHORING.ichaeyeon.md](AUTHORING.ichaeyeon.md)

---

## 📅 개발 기간

2026-05-04 ~ 2026-06-15 (6주)