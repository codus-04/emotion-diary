# ADR-0004 — UI 컴포넌트 스타일링 방식

| 항목 | 내용 |
|------|------|
| **상태** | ✅ Accepted |
| **결정일** | 2026.06.01 |

## 결정
React Native **StyleSheet API** 를 사용한다.

## 대안
- NativeWind (Tailwind CSS)
- Styled Components
- React Native Paper

## 이유
- 추가 라이브러리 없이 RN 기본 제공
- 성능 최적화 자동 적용
- 팀 학습 비용 최소화

## 결과
외부 의존성 없이 일관된 스타일 관리 가능
