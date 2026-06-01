# ADR-0005 — 로컬 데이터 저장 방식

| 항목 | 내용 |
|------|------|
| **상태** | ✅ Accepted |
| **결정일** | 2026.06.01 |

## 결정
**AsyncStorage** 를 로컬 캐시로 사용한다.

## 대안
- SQLite (expo-sqlite)
- MMKV
- SecureStore

## 이유
- Expo SDK 기본 지원
- 오프라인 일기 작성 가능
- 간단한 Key-Value 구조로 충분

## 결과
네트워크 없이도 일기 작성·조회 가능
