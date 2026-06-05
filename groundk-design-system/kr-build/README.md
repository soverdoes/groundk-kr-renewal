# `/kr` 홈 빌드 — 배포 가이드

영문 홈(`groundk.com`) 마크업을 **1:1로 복제**하고 한글 카피만 교체한 국문 홈입니다.
레이아웃·애니메이션 로직은 영문과 동일(같은 class 구조 + 동일 JS) → **90% 동일**.

## 파일
| 파일 | 배포 위치 |
|---|---|
| `index.html` | 서버의 `/kr/index.html` (라우트 `groundk.com/kr`) |
| `../overrides-ko.css` | `/resources/css/overrides-ko.css` |
| `en-home-source.html` | (참고용 원본, 배포 안 함) |

기존 자산(css/js/images/video)은 **영문과 공유** — 같은 `/resources/...` 경로라 추가 업로드 불필요.
유일한 신규 자산은 **`overrides-ko.css`** 하나.

## 영문 대비 변경점 (= 10%)
1. `<html lang="ko">`
2. `<head>`: title·description·OG·canonical 국문화, `og:locale ko_KR` + `alternate en_US`, hreflang 페어(`en` ↔ `ko-KR`), JSON-LD `inLanguage: ko`
3. `style.css` **뒤에** `overrides-ko.css` 추가 (한글 디스플레이 슬롯 행간/자간 보정, design-system §2.4)
4. 본문 카피 한글화 + 내부 링크 `/kr/...` 미러
5. **영문 유지(브랜드 장식)**: `WE MOVE YOU` / `Your Ground Travel Partner`(H1) / `DISCREET SAFE RELIABLE SERVICE` / 맵 도시 라벨 8종

## 동일 유지 (= 90%)
- 5섹션 구조·순서, 서비스 카드 4, 트러스트 카드 3, 맵 도시 8, `dark-theme` 클래스
- 클래스명·DOM 구조 100% 동일 → GSAP/ScrollTrigger/Lenis/Slick 애니메이션 그대로 동작
- 히어로 `.title` 3-span(`WE`/`MOVE`/`YOU`), welcome `comm-title` 2-`<p>` 등 JS가 참조하는 구조 보존

## 배포 후 검증 체크리스트
- [ ] `/kr` 진입 시 폰트 깨짐 없음 (한글 = Pretendard, 영문 장식 = Termina)
- [ ] welcome 하단 `DISCREET SAFE RELIABLE SERVICE` 아웃라인 정상, comm-title `지상 이동의 / 미래` 행간 안 잘림
- [ ] 서비스 카드3(전용 차량)·트러스트 카드3(로드쇼) 한글 длина로 카드 높이/줄바꿈 정상
- [ ] `자세히 보기` 버튼(고정 높이 45px) 텍스트 정렬 정상
- [ ] 맵 스크롤 인터랙션(라인/도트/txt-mask) 동작
- [ ] 모바일(portrait) GNB 풀스크린·푸터 정상
- [ ] hreflang 양방향: 영문 홈에도 `<link hreflang="ko-KR" href=".../kr">` 추가했는지 확인(상호 필수)

## 알아둘 점 (확인 필요)
- **H1이 영문**(`Your Ground Travel Partner`) — 결정에 따라 유지. 국문 SEO상 H1을 한글로 두는 게 유리하므로, 추후 검토 여지.
- **내부 링크는 `/kr` 미러 슬러그**(`/kr/airport-transfers` 등) 기준. 아직 국문 페이지 미빌드 시 404 → 빌드 전까지 임시로 영문 경로로 두거나 리다이렉트 매핑(i18n-spec §3) 적용.
- 트러스트/이벤트 링크: 독립 IA(통합) 확정 시 `/kr/business`·`/kr/events`로 교체 필요 (현재는 영문 미러 슬러그 유지).
- 영문 원본의 hreflang은 `/main`을 가리키는 부분이 있음 — 국문 추가 시 **영문 페이지의 hreflang도 정리**(en→`/`, ko-KR→`/kr`) 권장.
