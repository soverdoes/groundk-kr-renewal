# `/kr` 홈 신규 디자인 설계도 (디자인 시스템 기반)

> 방침: 영문 홈 미러를 **버리고**, GroundK 디자인 시스템(`design-system.md` · `tokens.css` · `overrides-ko.css`)만으로
> md(v10) 홈 콘텐츠 **전체**를 담는 새 국문 홈을 설계. 모든 신규 섹션도 **기존 토큰·간격·타입스케일·컬러·시그니처**로만 구성 → 룩앤필 100% 일관.

표기: 🔵 기존 컴포넌트 재사용 · 🟢 신규(디자인 시스템 토큰으로 신설) · sig=시그니처 효과

| # | 섹션 | md 블록 | 컴포넌트 | 테마 | 핵심 토큰 / 시그니처 |
|---|---|---|---|:--:|---|
| 1 | 히어로 | ① 히어로 | 🔵 `sct-design` + 🟢 eyebrow·CTA | dark | `WE MOVE YOU`(Termina, sig 유지) + `sub-title`(eyebrow, primary) + 국문 H1 + `comm-button`×2 + 배경 video |
| 2 | 미션 | ② OUR MISSION | 🔵 `sct-welcome` 패턴 | dark | `comm-title`(52) + 본문 + **`txt-stroke`** `WE MOVE YOU · WE DESIGN MOBILITY` (sig) |
| 3 | 핵심 수치 | ③ 50개국·300도시·491+·24/7 | 🟢 4-col stat band | light | 숫자=Termina `fs-52`, 라벨=`body-sm`/text-sub, 구분선=`.line`(border 0.2) |
| 4 | 서비스 2영역 | ④ 기업출장/해외이벤트 | 🔵 `sct-content` content-02(2-up) | light | 이미지+`tit`(32)+`desc`(20)+`comm-button`, gap `space-120` |
| 5 | 공감 Pain | ⑤ "이런 고민" 4카드 | 🟢 2×2 카드 | light | 카드 border 1px, `tit`(28/heading-2)+`desc`(20), radius-none |
| 6 | 다섯 약속 | ⑥ 5가지 약속 | 🟢 5-카드 그리드 | light | `sub-title`+`comm-title`, 5항목(전문성/24-7/편리/품질/투명) + 아이콘 `img-mask`(primary) |
| 7 | 서비스 | ⑦ 서비스 카드 | 🔵 `sct-services` 스티키 4카드 | dark | **스티키 스택**(sig) 4카드 + `comm-button`. JS 의존 → DOM 보존 |
| 8 | 네트워크 | ⑧ 인기 도시 | 🔵 `sct-worldwide` 맵 | light | **인터랙티브 맵**(sig, txt-mask 라벨 8) JS 의존 → DOM 보존 |
| 9 | Ground Partner | ⑨ 데이터/네트워크/맞춤 3카드 | 🔵 `sct-content` 3-col(`character`) | light | 아이콘 `img-mask` + `tit`(32) + `desc` |
| 10 | 프로젝트 사례 | ⑩ APEC/LV/BLACKPINK | 🔵 `descript-bg` 3 이미지카드 | light | 이미지 bg + scrim(black-50) + `tit`(32, white) + 수치 |
| 11 | 고객사 로고 | ⑪ 로고 | 🟢 로고 그리드 | light | 4그룹(정부/대기업/럭셔리/금융) 그레이 로고, gap `space-40` |
| 12 | CTA | ⑫ CTA | 🔵 `sct-banner` | dark | bg + scrim + `comm-title`(white) + `comm-button`×2 + 전화/이메일 + `txt-stroke` 워터마크 |

## 시그니처 보존 (JS 의존 섹션)
- **#7 스티키 서비스 스택**, **#8 인터랙티브 맵**, **#2 txt-stroke / txt-mask 스크롤 채움** → 기존 `main.js`/`common.js`가 정확한 DOM을 요구.
  → 이 섹션들은 기존 구조를 **그대로 유지**하고, 신규 섹션(③⑤⑥⑪)은 **CSS 전용/경량 스크롤리빌**로 추가해 JS 충돌 방지.
- 신규 스크롤 리빌이 필요하면 GSAP ScrollTrigger 재사용(이미 로드됨), 효과는 `0.3s ease-out` 1종 유지.

## 국문 타이포 규칙 (적용)
- 한글 = Pretendard, 영문 장식(`WE MOVE YOU`, 모토, 맵 라벨) = Termina (`overrides-ko.css` + `<html lang="ko">`).
- 신규 섹션 숫자(수치 띠)는 Termina 유지(영문/숫자), 한글 라벨은 Pretendard.

## 테마 리듬 (dark/light 교차)
`dark(1·2) → light(3·4·5·6) → dark(7) → light(8·9·10·11) → dark(12)`
(영문 홈의 dark-theme 교차 감각 계승)

## 산출 예정
1. `kr-build/home/index.html` — 12섹션 신규 홈
2. `kr-home.css` — 신규 섹션(③⑤⑥⑪ + 히어로 eyebrow/CTA) 스타일(토큰만 사용)
3. 기존 `style.css` + `overrides-ko.css` + 기존 JS 재사용

## 확정 필요 / 블로커
- [ ] **섹션 순서·포함 여부** 위 표대로 OK? (예: 5각형 그래픽은 v2로 미루고 5카드 그리드로 시작)
- [ ] **카피**: md가 mojibake라 실제 한글 문구 인용 불가 → **UTF-8 원본** 필요. (없으면 임시 한글로 뼈대만 잡고 추후 교체)
