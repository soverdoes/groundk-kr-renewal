# `/kr` 홈 — 영문 홈 1:1 미러 카피 맵

> 방침: **현재 영문 홈(`groundk.com`)의 5섹션·슬롯 구조를 100% 그대로 유지**하고 한글 카피만 교체.
> = 레이아웃 90% 동일. 나머지 10% = ①한글 타이틀 Termina→Pretendard 적응(§2.4) ②브랜드 영문 장식어 유지.
> 섹션 순서/개수/카드 수/도시 수 모두 영문과 동일하게 고정.

구조(영문=국문 동일):
`sct-design(dark)` → `sct-welcome(dark)` → `sct-services(dark, 카드 4)` → `sct-worldwide(맵, 도시 8)` → `sct-trusted(카드 3)`

---

## [1] sct-design — 히어로

| 슬롯 | 영문 원문 | 국문(복붙용) | 처리 |
|---|---|---|---|
| `.text .title` (대형) | **WE MOVE YOU** | **WE MOVE YOU** (유지) | Termina, 영문 브랜드 슬로건 — 교체 안 함 |
| `.image .title` (스크롤 등장) | Your Ground Travel Partner | Your Ground Travel Partner (유지) *또는* 당신의 그라운드 파트너 | 유지 권장(영문 장식) |

> 영문 슬로건은 디자인 정체성이라 **그대로 유지**. 한글 병기를 원하면 `.image .title`만 국문화.

---

## [2] sct-welcome

| 슬롯 | 영문 원문 | 국문(복붙용) | 처리 |
|---|---|---|---|
| `.comm-title` | The Future of Ground Transportation | 지상 이동의 미래 | Pretendard 700(§2.4) |
| `.descript .desc` | GroundK is the leader in chauffeured services and ground transportation logistics management in Korea, providing full end-to-end solutions for the most discerning travelers and maintaining its highest quality and safety standards through innovation, dedication to the customer, and personal and professional service. | GroundK는 한국을 대표하는 쇼퍼 드리븐 서비스·지상 교통 물류 관리 기업입니다. 가장 안목 높은 고객을 위한 엔드투엔드 솔루션을 제공하며, 혁신과 고객을 향한 헌신, 섬세하고 전문적인 서비스로 최고 수준의 품질과 안전 기준을 유지합니다. | 본문 20px/text-sub |
| `.txt-stroke` | DISCREET SAFE RELIABLE SERVICE | DISCREET SAFE RELIABLE SERVICE (유지) *또는* 신중함 · 안전 · 신뢰 | 유지 권장(Termina 아웃라인 장식) |
| 이미지 3종 | (장식) | 동일 | 변경 없음 |

---

## [3] sct-services — 카드 4개 (고정)

| 슬롯 | 영문 | 국문(복붙용) |
|---|---|---|
| `.comm-title` | Our Services | 서비스 |
| 카드1 `.tit` | Airport Transfers | 공항 픽업 |
| 카드1 `.desc` | Aiming to achieve the highest standards to deliver an exclusive and reliable chauffeur service for local and international flights. | 국내외 항공편을 위한 정확하고 신뢰할 수 있는 최고 수준의 쇼퍼 서비스를 제공합니다. |
| 카드2 `.tit` | Airport Concierge | 공항 컨시어지 |
| 카드2 `.desc` | To make your arrival special | 당신의 도착을 특별하게. |
| 카드3 `.tit` | As-Directed Service | 전용 차량 |
| 카드3 `.desc` | GroundK chauffeur services offer you tailored safe and reliable transport from hours to full day. | 시간 단위부터 종일까지, 일정에 맞춘 안전하고 신뢰할 수 있는 맞춤 이동을 제공합니다. |
| 카드4 `.tit` | Shuttle Service | 셔틀 서비스 |
| 카드4 `.desc` | Stress-free schedules and efficient routes will keep your people connected and pleasant daily life. | 스트레스 없는 일정과 효율적인 동선으로 구성원의 이동과 일상을 쾌적하게 연결합니다. |
| `.btn` ×4 | see more | 자세히 보기 |

> 링크: 카드1→`/kr/airport-transfers`, 카드2→`/kr/airport-concierge`, 카드3→`/kr/as-directed-service`, 카드4→`/kr` (셔틀 국문 페이지 미정 시 임시 `/kr` 또는 영문 `/shuttle-service`).

---

## [4] sct-worldwide — 인터랙티브 맵 (도시 8개 고정)

| 슬롯 | 영문 | 국문(복붙용) |
|---|---|---|
| `.comm-title` | GroundK Destination | GroundK 네트워크 |
| 맵 라벨 ×8 | Shanghai · Dubai · Seoul · Tokyo · Bangkok · Singapore · Sydney · Hong Kong | **영문 유지 권장** / (국문 시) 상하이 · 두바이 · 서울 · 도쿄 · 방콕 · 싱가포르 · 시드니 · 홍콩 |

> 맵 라벨은 Termina로 스타일된 시각 요소라 **영문 유지가 디자인상 안전**. 한글로 바꾸면 §2.4 폴백(Pretendard)로 렌더되며 라벨 위치/폭 미세 조정 필요.

---

## [5] sct-trusted — 카드 3개 (고정)

| 슬롯 | 영문 | 국문(복붙용) |
|---|---|---|
| `.comm-title` | Your Ground Travel Partner | 당신의 그라운드 트래블 파트너 |
| 카드1 `.tit` | Corporate Travel | 기업 출장 |
| 카드1 `.desc` | Consistent, reliable, and outstanding service. Specialized in providing corporate transportation solutions for your business. GroundK chauffeur service helps you to handle important matters. | 일관되고 신뢰할 수 있는 탁월한 서비스. 비즈니스를 위한 기업 이동 솔루션을 전문적으로 제공하여, 중요한 업무에 집중하실 수 있도록 돕습니다. |
| 카드2 `.tit` | Events | 이벤트 |
| 카드2 `.desc` | From small groups to large-scale events, GroundK understands the unique nature of events, and our dedicated managers ensure your event is successful. Trust GroundK for all your event planning needs. | 소규모 그룹부터 대규모 행사까지, GroundK는 이벤트의 고유한 특성을 이해하며 전담 매니저가 행사의 성공을 보장합니다. 모든 이벤트 수송을 GroundK에 맡기십시오. |
| 카드3 `.tit` | Road Shows | 로드쇼 |
| 카드3 `.desc` | GroundK has a talented team of roadshow coordinators who understand the bespoke requirements of our customers. We monitor and track real-time flight schedules and vehicle locations to ensure seamless meeting schedules that are efficient and can adjust to any challenges. | 고객 맞춤 요구를 이해하는 전문 로드쇼 코디네이터 팀이 실시간 항공 일정과 차량 위치를 추적하여, 어떤 변수에도 대응하는 효율적이고 매끄러운 미팅 일정을 보장합니다. |
| `.btn` ×3 | see more | 자세히 보기 |

> 링크: 카드1→`/kr/business`, 카드2→`/kr/events`, 카드3→`/kr/business#roadshow` (국문 IA 기준).

---

## 적용 체크 (10% 적응분)

- [ ] `<html lang="ko">` + `overrides-ko.css`를 `style.css` 뒤에 로드 (§2.4)
- [ ] 영문 유지 장식어: `WE MOVE YOU`, `DISCREET SAFE RELIABLE SERVICE`, 맵 도시 라벨 → Termina 그대로
- [ ] 국문 타이틀(`comm-title` 등)은 Pretendard 700 자동 렌더 + 행간 완화 확인 (잘림 없는지)
- [ ] `.desc` 본문 길이: 영문 대비 한글이 길어질 수 있음 → 카드 높이 sticky 레이아웃에서 줄바꿈 확인(특히 services 카드3·trusted 카드3)
- [ ] `see more` → `자세히 보기` 폭 변화로 버튼(`.comm-button` 고정 높이 45px) 내 정렬 확인
- [ ] 섹션 `dark-theme` 클래스 유지(영문과 동일)

## 미세 결정 3건 (확정 필요)
1. 히어로 `Your Ground Travel Partner` → 영문 유지 / 국문 병기?
2. `DISCREET SAFE RELIABLE SERVICE` → 영문 유지 / `신중함·안전·신뢰`?
3. 맵 도시 라벨 → 영문 유지 / 국문(상하이…)?

_기준: groundk.com 현행 홈 + §2.4 국문 규칙. 생성 2026-06-02._
