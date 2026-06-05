# GroundK i18n — URL · hreflang · 페이지 빌드 명세

> 결정사항 (2026-06-02)
> - **IA 정책**: 국문 독립 IA. 국문은 v10 콘텐츠 문서 구조를 따르고, 영문은 현행 19개 페이지 유지.
> - **경로**: 영문 = 루트 `groundk.com/…`, 국문 = `groundk.com/kr/…`
> - **hreflang**: `ko-KR` (경로는 `/kr`, 검색엔진 신호는 `ko-KR`). 영문 = `en`, 기본 = `x-default`(영문 루트).
> - hreflang은 **양 언어에 실제로 존재하는 페이지끼리만** 양방향 연결. 나머지는 self-canonical.

---

## 1. URL 인벤토리

### 1-A. 영문 (루트) — 현행 유지, 변경 없음
`/` · `/airport-transfers` · `/airport-concierge` · `/as-directed-service` · `/shuttle-service`
`/corporate-travel` · `/road-show`
`/sports-entertainments` · `/luxury-events` · `/international-summit` · `/conferences-conventions` · `/case-studies`
`/cities-worldwide` · `/our-professional` · `/our-global-fleet` · `/sustainability` · `/contact-us`
`/term-conditions` · `/privacy-policy`

### 1-B. 국문 (`/kr`) — v10 문서 IA
`/kr` · `/kr/booking`(Phase 3)
`/kr/airport-transfers` · `/kr/airport-concierge` · `/kr/as-directed-service`
`/kr/business`(기업출장+로드쇼 통합, 앵커 `#roadshow`)
`/kr/events`(이벤트 통합)
`/kr/case-studies` · `/kr/cities-worldwide` · `/kr/our-professional` · `/kr/contact-us`
`/kr/guide` · `/kr/faq`

---

## 2. hreflang 매핑

### 2-A. 양방향 연결 페어 (8) — 양쪽 모두 존재
| 영문 | 국문 |
|---|---|
| `/` | `/kr` |
| `/airport-transfers` | `/kr/airport-transfers` |
| `/airport-concierge` | `/kr/airport-concierge` |
| `/as-directed-service` | `/kr/as-directed-service` |
| `/case-studies` | `/kr/case-studies` |
| `/cities-worldwide` | `/kr/cities-worldwide` |
| `/our-professional` | `/kr/our-professional` |
| `/contact-us` | `/kr/contact-us` |

각 페어의 `<head>` (양쪽에 **상호** 삽입):
```html
<link rel="alternate" hreflang="en"        href="https://groundk.com/{slug}">
<link rel="alternate" hreflang="ko-KR"     href="https://groundk.com/kr/{slug}">
<link rel="alternate" hreflang="x-default" href="https://groundk.com/{slug}">
<link rel="canonical"                      href="https://groundk.com/{현재 페이지 자기 URL}">
```

### 2-B. 영문 전용 (self-canonical, hreflang alternate 없음)
`/shuttle-service` · `/corporate-travel` · `/road-show` · `/sports-entertainments` · `/luxury-events` · `/international-summit` · `/conferences-conventions` · `/our-global-fleet` · `/sustainability` · `/term-conditions` · `/privacy-policy`
```html
<link rel="canonical" href="https://groundk.com/{slug}">
<!-- 국문 번역 생성 시 해당 페이지와 양방향 hreflang 추가 -->
```

### 2-C. 국문 전용 (self-canonical, hreflang alternate 없음)
`/kr/business` · `/kr/events` · `/kr/guide` · `/kr/faq` · `/kr/booking`
```html
<link rel="canonical" href="https://groundk.com/kr/{slug}">
```

> **원칙**: 짝 없는 페이지에 상대 언어 URL을 hreflang으로 걸지 말 것(잘못된 매핑 = 색인 오류). 번역이 추가되는 시점에만 연결.

---

## 3. 언어 전환 버튼(Language Switcher) 폴백 규칙

GNB/Footer의 KOR|ENG 토글은 짝 없는 페이지에서 404가 나면 안 됨. 폴백 우선순위:

| 현재 위치 | 토글 시 이동 |
|---|---|
| 페어 존재 페이지 | 1:1 상대 URL |
| EN `/corporate-travel`, `/road-show` → KR | `/kr/business` (통합 대응 페이지) |
| EN `/sports-entertainments` 등 이벤트 5종 → KR | `/kr/events` |
| EN `/shuttle-service`·`/our-global-fleet`·`/sustainability`·약관 → KR | `/kr` (국문 홈) + 토스트 "해당 페이지는 곧 제공됩니다" |
| KR `/kr/business`·`/kr/events`·`/kr/guide`·`/kr/faq` → EN | 가장 근접한 EN 페이지(예: business→`/corporate-travel`) 또는 EN 루트 |

매핑 테이블을 JSON으로 관리 권장 (라우터/미들웨어에서 참조):
```json
{
  "en2kr": { "/corporate-travel": "/kr/business", "/road-show": "/kr/business#roadshow",
             "/sports-entertainments": "/kr/events", "/luxury-events": "/kr/events",
             "/international-summit": "/kr/events", "/conferences-conventions": "/kr/events",
             "/shuttle-service": "/kr", "/our-global-fleet": "/kr",
             "/sustainability": "/kr", "/term-conditions": "/kr", "/privacy-policy": "/kr" },
  "kr2en": { "/kr/business": "/corporate-travel", "/kr/events": "/case-studies",
             "/kr/guide": "/", "/kr/faq": "/", "/kr/booking": "/" }
}
```

---

## 4. 국문 페이지별 빌드 방식 (기존 디자인 시스템 재사용 관점)

> 목표: "현재 디자인·레이아웃 안 깨지게". 기존 컴포넌트(=design-system.md §6)를 최대한 재사용. ⬜=신규 디자인 필요.

| 국문 페이지 | 재사용 가능 템플릿/컴포넌트 | 신규 필요 | 난이도 |
|---|---|---|---|
| `/kr` HOME | sct-design·welcome·services(**4칸 고정**)·worldwide(맵 8도시)·trusted(3칸) | 핵심수치 띠, 5각형 가치, 프로젝트사례 카드, 로고 그리드 | 中 |
| `/kr/airport-transfers` | visual + character(**3칸**) + content-01 + banner | 5단계 플로우는 character로 못 담음 → step 컴포넌트 차용 | 低 |
| `/kr/airport-concierge` | visual + content×2 + banner | 프로세스표(3×5), 등급 비교표, FAQ 아코디언 | 中 |
| `/kr/as-directed-service` | visual + content-01 + character(**3칸**) + banner | 시나리오 6개 → 슬롯 초과분 처리 | 低 |
| `/kr/business` | visual·character(3)·content-03/04/05·banner | **앵커 탭 네비**(기업출장/로드쇼), 로드쇼 일정표 | 中~高 |
| `/kr/events` | visual·character·content·review·banner·gallery | **이벤트 타입 카드, 타임라인(D-30), 멀티베뉴, FAQ** | 高 |
| `/kr/case-studies` | sct-gallery(필터+그리드) | — | 低 |
| `/kr/cities-worldwide` | sct-map(국가 2열 그리드) | — | 低 |
| `/kr/our-professional` | content×3 | 핵심수치, 5각형, 5단계 프로세스, 데이터 리포트 블록 | 高 |
| `/kr/contact-us` | sct-contact | — | 低 |
| `/kr/guide` | **sct-step**(번호 스텝) + 차량등급 표 + 포함내역 표 | 표 2종 | 低 |
| `/kr/faq` | **sct-accordion** + sct-title (약관 페이지와 동일 컴포넌트) | — | 低 |
| `/kr/booking` | — | T-RiseUp 예약 위젯(Phase 3) | — |

**바로 착수 가능(低)**: case-studies, cities-worldwide, contact-us, guide, faq, airport-transfers, as-directed-service
**부분 신규(中)**: home, airport-concierge, business
**신규 설계 비중 큼(高)**: events, our-professional

---

## 5. 공통 체크리스트 (개발 전달)
- [ ] 모든 `/kr` 페이지 `<html lang="ko">` (영문은 `lang="en">`)
- [ ] sitemap.xml에 hreflang `xhtml:link` 포함(페어 8쌍만 상호), 국문/영문 URL 모두 등재
- [ ] 짝 없는 페이지 self-canonical 확인(상대 언어 hreflang 금지)
- [ ] 언어 토글 폴백 매핑(JSON) 적용, 404 방지
- [ ] OG/Twitter 메타 `og:locale` = `en_US` / `ko_KR`, `og:locale:alternate` 상호
- [x] 폰트: 한글 Termina 슬롯 → Pretendard 700 대체 규칙 **확정** (design-system §2.4, `tokens.css` 폴백 + `overrides-ko.css`). `/kr`에서 `<html lang="ko">` + `overrides-ko.css`를 `style.css` 뒤에 로드
- [ ] meta title/description 국문본은 v10 문서 부록 D-1 사용( `/ko`→`/kr` 치환 )

---

_생성: 2026-06-02. 기준: groundk.com 현행 빌드 + 콘텐츠 카피 v10._
