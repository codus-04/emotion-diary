# 02. WBS (Work Breakdown Structure)

## 프로젝트명
AI 감정일기 (Emotion Diary)

## 작성일
2026-05-04

---

## 1. 프로젝트 관리
- 1.1 요구사항 정의 및 문서화
- 1.2 일정 관리 및 주차별 목표 설정
- 1.3 GitHub 리포지토리 관리
- 1.4 발표 준비

---

## 2. 환경 설정
- 2.1 Flutter 개발 환경 구성
- 2.2 GitHub 리포지토리 생성 및 초기 커밋
- 2.3 Claude API Key 발급 및 .env 설정
- 2.4 Flutter 패키지 설치 (pubspec.yaml)
- 2.5 CI/CD 파이프라인 구성 (GitHub Actions)
- 2.6 Firebase App Distribution 설정

---

## 3. 문서화
- 3.1 00-vision.md 작성
- 3.2 01-requirements.md 작성 (MoSCoW)
- 3.3 02-wbs.md 작성
- 3.4 04-schedule.md 작성
- 3.5 ADR-001 플랫폼 선택 근거
- 3.6 ADR-002 AI 모델 선택 근거
- 3.7 ADR-003 감정 분석 방식 선택 근거
- 3.8 docs/architecture.md 작성
- 3.9 docs/setup.md 작성
- 3.10 docs/deploy.md 작성
- 3.11 docs/testing.md 작성
- 3.12 AGENTS.md 작성
- 3.13 AUTHORING.md 작성
- 3.14 README.md 작성

---

## 4. 프로젝트 구조 설계
- 4.1 Clean Architecture 레이어 설계
  - 4.1.1 core/ (공통 유틸, 상수, 테마)
  - 4.1.2 data/ (API 호출, 로컬 DB)
  - 4.1.3 domain/ (비즈니스 로직, 감정 분석)
  - 4.1.4 presentation/ (UI 레이어, 상태관리)
- 4.2 라우팅 구조 설계
- 4.3 상태관리 구조 설계 (Riverpod)

---

## 5. UI 구현
- 5.1 디자인 시스템 설정 (색상, 폰트, 테마)
- 5.2 홈 화면 (오늘의 감정 + 최근 일기 목록)
- 5.3 일기 작성 화면
  - 5.3.1 텍스트 입력 폼
  - 5.3.2 음성 입력 버튼
  - 5.3.3 감정 태그 선택 UI
- 5.4 일기 상세 화면
- 5.5 감정 그래프 화면 (주간/월간)
- 5.6 설정 화면 (알림 시간 설정 등)

---

## 6. 기능 구현
- 6.1 일기 CRUD
  - 6.1.1 일기 작성
  - 6.1.2 일기 조회
  - 6.1.3 일기 수정
  - 6.1.4 일기 삭제
- 6.2 음성 입력
  - 6.2.1 flutter_speech_to_text 연동
  - 6.2.2 음성 → 텍스트 변환
- 6.3 Claude API 감정 분석
  - 6.3.1 API 호출 모듈 구현
  - 6.3.2 감정 레이블 파싱
  - 6.3.3 감정 점수 산출
- 6.4 로컬 DB 연동 (Isar)
  - 6.4.1 스키마 정의
  - 6.4.2 CRUD 구현
- 6.5 감정 시각화
  - 6.5.1 주간 감정 그래프 (fl_chart)
  - 6.5.2 월간 감정 캘린더
- 6.6 푸시 알림 (flutter_local_notifications)

---

## 7. 테스트
- 7.1 단위 테스트
  - 7.1.1 감정 분석 로직 테스트
  - 7.1.2 Isar DB CRUD 테스트
- 7.2 위젯 테스트
  - 7.2.1 일기 입력 폼 테스트
  - 7.2.2 감정 그래프 렌더링 테스트
- 7.3 통합 테스트
  - 7.3.1 일기 작성 → 감정 분석 → 저장 전체 흐름

---

## 8. 배포
- 8.1 GitHub Actions 빌드 자동화
- 8.2 Firebase App Distribution 배포
- 8.3 최종 빌드 검증