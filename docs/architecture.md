# Architecture

## 프로젝트명
AI 감정일기 (Emotion Diary)

## 작성일
2026-05-04

---

## 전체 시스템 구조
┌─────────────────────────────────────────┐
│              Flutter App                │
│                                         │
│  ┌──────────┐      ┌──────────────────┐ │
│  │    UI    │ ←──→ │   Riverpod       │ │
│  │ (Screens)│      │   (State Mgmt)   │ │
│  └──────────┘      └────────┬─────────┘ │
│                             │           │
│  ┌──────────────────────────▼─────────┐ │
│  │           Domain Layer             │ │
│  │   (비즈니스 로직 / 감정 분석)        │ │
│  └──────────────────────────┬─────────┘ │
│                             │           │
│  ┌──────────────────────────▼─────────┐ │
│  │            Data Layer              │ │
│  │   ┌─────────────┐ ┌─────────────┐  │ │
│  │   │  Isar (DB)  │ │ Claude API  │  │ │
│  │   └─────────────┘ └─────────────┘  │ │
│  └────────────────────────────────────┘ │
└─────────────────────────────────────────┘
│                    │
┌──────▼──────┐    ┌────────▼───────┐
│  Local DB   │    │  Anthropic API │
│   (Isar)    │    │ claude-haiku   │
└─────────────┘    └────────────────┘

---

## 레이어 구조 (Clean Architecture)

### Presentation Layer
- UI 컴포넌트 및 화면 담당
- Riverpod Provider로 상태 관리
- 사용자 입력 처리 및 화면 렌더링
lib/presentation/
├── screens/
│   ├── home_screen.dart         # 홈 화면 (일기 목록)
│   ├── diary_write_screen.dart  # 일기 작성 화면
│   ├── diary_detail_screen.dart # 일기 상세 화면
│   ├── chart_screen.dart        # 감정 그래프 화면
│   └── settings_screen.dart     # 설정 화면
├── widgets/
│   ├── emotion_tag.dart         # 감정 태그 위젯
│   ├── diary_card.dart          # 일기 카드 위젯
│   └── emotion_chart.dart       # 감정 차트 위젯
└── providers/
├── diary_provider.dart      # 일기 상태 관리
└── emotion_provider.dart    # 감정 분석 상태 관리

### Domain Layer
- 핵심 비즈니스 로직 담당
- UI와 데이터 레이어로부터 독립
- 감정 분석 결과 가공 및 패턴 계산
lib/domain/
├── models/
│   ├── diary_entry.dart         # 일기 모델
│   └── emotion_result.dart      # 감정 분석 결과 모델
├── usecases/
│   ├── save_diary.dart          # 일기 저장 유스케이스
│   ├── analyze_emotion.dart     # 감정 분석 유스케이스
│   └── get_emotion_trend.dart   # 감정 트렌드 조회
└── repositories/
├── diary_repository.dart    # 일기 저장소 인터페이스
└── emotion_repository.dart  # 감정 분석 저장소 인터페이스

### Data Layer
- 외부 데이터 소스 연동 담당
- Isar DB (로컬 저장) + Claude API (감정 분석)
lib/data/
├── local/
│   ├── isar_service.dart        # Isar DB 초기화
│   └── diary_dao.dart           # 일기 CRUD
├── remote/
│   ├── claude_api_service.dart  # Claude API 호출
│   └── emotion_parser.dart      # 감정 분석 결과 파싱
└── repositories/
├── diary_repository_impl.dart
└── emotion_repository_impl.dart

### Core
- 공통 유틸리티, 상수, 테마 담당
lib/core/
├── constants/
│   ├── app_colors.dart          # 색상 상수
│   └── emotion_labels.dart      # 감정 레이블 상수
├── theme/
│   └── app_theme.dart           # 앱 테마 설정
└── utils/
├── date_formatter.dart      # 날짜 포맷 유틸
└── env_config.dart          # 환경변수 로드

---

## 주요 패키지

| 패키지 | 버전 | 용도 |
|---|---|---|
| flutter_riverpod | ^2.5.0 | 상태 관리 |
| isar | ^3.1.0 | 로컬 DB |
| go_router | ^13.0.0 | 화면 라우팅 |
| flutter_speech_to_text | ^6.6.0 | 음성 입력 |
| fl_chart | ^0.68.0 | 감정 그래프 |
| http | ^1.2.0 | Claude API 호출 |
| flutter_dotenv | ^5.1.0 | 환경변수 관리 |
| flutter_local_notifications | ^17.0.0 | 푸시 알림 |

---

## 감정 분석 데이터 흐름

사용자 일기 작성 (텍스트 or 음성)
↓
Isar DB에 일기 원문 저장
↓
Claude API에 감정 분석 요청
↓
감정 결과 수신 (JSON)
{
"primary_emotion": "슬픔",
"emotions": ["슬픔", "불안"],
"score": 28,
"summary": "힘든 하루를 보낸 것 같아요"
}
↓
Isar DB 감정 데이터 업데이트
↓
UI 감정 태그 + 그래프 반영


---

## 보안 설계

| 항목 | 방식 |
|---|---|
| API Key 관리 | .env 파일 + flutter_dotenv (git 제외) |
| 로컬 DB 암호화 | Isar 암호화 옵션 적용 |
| 네트워크 통신 | HTTPS only |
| 개인정보 | 일기 원문 서버 미보관 |

---

## 관련 문서
- [ADR-001-플랫폼선택.md](../.planning/decisions/ADR-001-플랫폼선택.md)
- [ADR-002-AI모델선택.md](../.planning/decisions/ADR-002-AI모델선택.md)
- [ADR-003-감정분석방식.md](../.planning/decisions/ADR-003-감정분석방식.md)