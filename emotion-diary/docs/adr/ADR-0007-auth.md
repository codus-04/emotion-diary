# ADR-0007 — 사용자 인증 방식

| 항목 | 내용 |
|------|------|
| **상태** | ✅ Accepted |
| **결정일** | 2026.06.01 |

## 결정
**Firebase Authentication** 을 사용한다.

## 대안
- 자체 JWT 서버
- Supabase Auth
- Auth0

## 이유
- 이메일·Google·Apple 로그인 즉시 지원
- JWT 토큰 자동 관리
- Firestore 보안 규칙과 통합 용이

## 결과
5분 안에 소셜 로그인 구현 가능
