# groundk.com/ko — Contents Copy Final 통합본 v10

> _[기획서 · 디자인 미적용 · 콘텐츠 100% 원문]_


> **Status**: Production-Ready · 개발팀·디자인팀 전달용
> **Last Updated**: 2026.06.02
> **Scope**: 글로벌 Chauffeur Service (해외 출장 차량 + 해외 이벤트 수송)

---

## v10 변경사항 총괄

| # | 페이지 | 변경 | 요약 |
|---|--------|------|------|
| 1 | HOME | UPDATE | Pain 카드 재구성, YGP 브릿지 구체화, 서비스 카드 보강 |
| 2 | 공항 픽업 | UPDATE | 패스트트랙 연결 카드 추가 |
| 3 | 공항 패스트트랙 | **REWRITE** | 5→9섹션. 도착/출발/환승 상세, 공항픽업 연계, 이용대상 6종, FAQ |
| 4 | 비즈니스 | NEW +2 | 해외 출장 Pain, 해외에서도 같은 매니저 |
| 5 | 이벤트 | **REWRITE** | 8→12섹션. 해외 행사 Pain, 브릿지 역할, 현장 운영, 데이터 |
| 6 | 전문 역량 | NEW +3 | 글로벌 운영 역량, 운영 체계, 데이터 기반 운영, 스케일 4단 |
| 7 | FAQ | UPDATE | 패스트트랙·이벤트 Q&A 추가 |
| 8 | 부록 | UPDATE | 메시지 위계 Layer 보강, 페르소나 매핑 업데이트, 메타 데이터 추가 |

## 8개 전문가 관점 교차 검토 — 핵심 반영 사항

| 관점 | 핵심 반영 |
|------|---------|
| **R1. PCO·MICE PM** | 이벤트: 해외 행사 Pain 4건 + 브릿지 역할 5건. "현장에 누가 나옵니까?" 답변. |
| **R2. 브랜드·엔터 디렉터** | "브랜드의 행사 경험을 수송까지 일관되게." Quiet Luxury 톤 유지. |
| **R3. 기업 총무팀장** | 비즈니스: 해외 출장 Pain 신설. "매니저가 현지 기사를 대신 관리." |
| **R4. 마케팅 전략가** | 모든 페이지 Pain→Solution→Proof→CTA 흐름. 중간 CTA 삽입. |
| **R5. 글로벌 TMS 마케팅 디렉터** | "기존 출장 여행사와 병행 가능." FAQ에 TMC 연계 Q&A 보강. 통합 정산·Duty of Care 강조. |
| **R6. UX·콘텐츠 전략가** | 서비스 간 교차 링크(패스트트랙↔픽업↔전용차량). 섹션별 배경 교차(Dark/Light/Alt). |
| **R7. 브랜드 일관성** | "5초 GPS" 0건 확인. 용어 표준 준수. 경쟁사 직접 언급 0건. |
| **R8. SEO** | 모든 서비스 페이지에 FAQ 추가. 메타 태그 전 페이지 완비. AI 검색 인용 최적화 구조. |

---

## 0. 통합본 개요

**메시지 위계 (Site Voice Hierarchy)**

```
Layer 1 (Mission)         이동 경험을 디자인합니다 · WE MOVE YOU
Layer 2 (Positioning)     Your Ground Partner · Trusted Business Partner
Layer 3 (Brand Pillars)   전문성 · 24/7 · 편리한 운영 · 서비스 품질관리 · 투명성
Layer 4 (Differentiation) 데이터 기반 기술 + 글로벌 네트워크 + 맞춤 설계
                          = 한국의 기준, 해외 현지에서도 (v10 강화)
Layer 5 (Proof)           50개국·300개 도시·491+ 기업·APEC·정상회의·BLACKPINK
```

**페르소나 (Marketing Target)**

```
A-1. 총무·경영지원 팀장      (계약 의사결정자)
A-2. 비서실·예약 담당         (일상 사용자)
A-3. IR·글로벌 비즈니스 리더  (로드쇼 책임자)
A-4. 출장 임원·C-level        (End User)
B-1. PCO·MICE 에이전시 PM     (이벤트 파트너)
B-2. 브랜드·엔터 이벤트 디렉터 (이벤트 파트너)
```