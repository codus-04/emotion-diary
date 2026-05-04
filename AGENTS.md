# AGENTS.md

## 프로젝트명
AI 감정일기 (Emotion Diary)

## 작성일
2026-05-04

---

## 이 파일의 목적
이 프로젝트에서 AI Agent (Claude)를 어떻게 활용했는지,
그리고 앞으로 어떻게 활용할지를 정의하는 문서입니다.
AI가 생성한 코드와 문서에 대해 본인이 책임지고 관리합니다.

---

## 1. AI Agent 활용 범위

### 문서 생성
| 문서 | AI 활용 방식 | 본인 검토 여부 |
|---|---|---|
| 00-vision.md | Claude로 초안 생성 후 직접 수정 | ✅ |
| 01-requirements.md | Claude로 MoSCoW 초안 생성 후 직접 수정 | ✅ |
| 02-wbs.md | Claude로 태스크 분해 후 직접 수정 | ✅ |
| 04-schedule.md | Claude로 6주 일정 초안 생성 후 직접 수정 | ✅ |
| ADR-001 ~ 003 | Claude로 초안 생성 후 직접 수정 | ✅ |
| architecture.md | Claude로 구조 설계 초안 생성 후 직접 수정 | ✅ |
| setup.md | Claude로 초안 생성 후 직접 수정 | ✅ |
| deploy.md | Claude로 초안 생성 후 직접 수정 | ✅ |
| testing.md | Claude로 초안 생성 후 직접 수정 | ✅ |

### 코드 생성
| 영역 | AI 활용 방식 |
|---|---|
| Flutter 프로젝트 구조 | Claude로 Clean Architecture 구조 설계 |
| Claude API 연동 코드 | Claude로 초안 생성 후 직접 테스트 및 수정 |
| Isar DB 스키마 | Claude로 초안 생성 후 직접 검증 |
| 테스트 코드 | Claude로 초안 생성 후 직접 실행 및 수정 |
| GitHub Actions 워크플로우 | Claude로 초안 생성 후 직접 검증 |

---

## 2. AI Agent 활용 원칙

### 반드시 지키는 규칙
1. **AI 생성물은 반드시 직접 읽고 검토한다**
   - 코드는 직접 실행해서 동작을 확인한다
   - 문서는 내용이 프로젝트와 일치하는지 확인한다

2. **AI가 만든 부분을 정직하게 밝힌다**
   - 커밋 메시지에 AI 활용 여부를 명시한다
   - 발표 Q&A에서 AI가 만든 부분을 솔직히 말한다

3. **AI 출력을 그대로 쓰지 않는다**
   - 초안을 받은 후 반드시 본인 상황에 맞게 수정한다
   - 빈 파일이나 템플릿 상태로 커밋하지 않는다

4. **모르는 코드는 이해하고 넘어간다**
   - AI가 생성한 코드에서 모르는 부분은 Claude에게 설명을 요청한다
   - Q&A에서 답할 수 있는 수준으로 이해한 후 커밋한다

---

## 3. AI Agent 활용 프롬프트 기록

### 문서 작성 프롬프트 패턴
"AI 감정일기 앱의 {문서명} 작성해줘.
{포함할 내용}을 포함해서 마크다운으로 작성해줘."

### 코드 생성 프롬프트 패턴
"Flutter + Claude API로 만드는 감정일기 앱에서
{기능명} 구현 코드 작성해줘.
Clean Architecture 구조로, Riverpod 상태관리 사용해서."

### 오류 해결 프롬프트 패턴
"아래 오류가 발생했어. 원인과 해결 방법 알려줘.
{오류 메시지}"

---

## 4. AI가 잘하는 것 vs 직접 해야 하는 것

| AI가 잘하는 것 | 직접 해야 하는 것 |
|---|---|
| 문서 초안 빠르게 생성 | 프로젝트에 맞게 내용 수정 |
| 보일러플레이트 코드 생성 | 실제 실행 및 동작 검증 |
| 오류 원인 분석 | 오류 수정 후 재실행 확인 |
| 테스트 코드 초안 생성 | 테스트 실행 및 결과 확인 |
| 아키텍처 설계 제안 | 프로젝트 요구사항에 맞게 조정 |

---

## 5. 커밋 메시지 규칙

AI 활용 여부를 커밋 메시지에 명시합니다:
AI 초안 생성 후 수정한 경우
docs: 00-vision.md 작성 (Claude 초안 + 직접 수정)
직접 작성한 경우
docs: ADR-001 플랫폼 선택 근거 작성
AI 생성 코드를 검증 후 사용한 경우
feat: Claude API 감정 분석 연동 (AI 생성 + 직접 검증)

---

## 6. 참고 도구

| 도구 | 용도 |
|---|---|
| Claude (claude.ai) | 문서 초안, 코드 생성, 오류 해결 |
| GitHub Copilot | VS Code 내 코드 자동완성 |
| Claude API | 앱 내 감정 분석 기능 |

---

## 관련 문서
- [AUTHORING.ichaeyeon.md](AUTHORING.ichaeyeon.md)
- [README.md](README.md)
- [docs/architecture.md](docs/architecture.md)