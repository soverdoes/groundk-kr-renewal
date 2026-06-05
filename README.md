# GroundK — 국문(/kr) 페이지 리뉴얼

groundk.com 국문 전용 페이지(`/kr`) 리뉴얼 작업물입니다. 디자인 시스템, 페이지 빌드(HTML/CSS), 기획 문서를 포함합니다.

## 🌐 라이브 미리보기

**https://soverdoes.github.io/groundk-kr-renewal/kr/**

| 페이지 | 경로 |
|---|---|
| 홈 (메인) | `/kr/` |
| 공항 픽업 | `/kr/airport-transfers/` |
| 공항 패스트트랙 | `/kr/airport-concierge/` |
| 전용차량 | `/kr/as-directed-service/` |
| 비즈니스 | `/kr/business/` |
| 이벤트 | `/kr/events/` |
| 프로젝트 사례 | `/kr/case-studies/` |
| 서비스 지역 | `/kr/cities-worldwide/` |
| 문의하기 | `/kr/contact-us/` |
| 이용 가이드 | `/kr/guide/` |
| FAQ | `/kr/faq/` |
| 전문 역량 | `/kr/our-professional/` |
| 바로 예약 | `/kr/booking/` |

> 메인 홈은 Figma "Frame 1"(직접 디자인) 기준으로 13개 섹션을 1:1 재현했습니다.
> 이미지는 모두 **파일명 빈 박스(placeholder)** 이며, 실제 이미지로 교체 예정입니다.
> 서브페이지 스타일은 운영 사이트 CSS(groundk.com CDN)를 불러오므로 인터넷 연결 시 정상 표시됩니다.

## 📁 구조

```
docs/                         # GitHub Pages 배포본 (경로 프리픽스 보정)
groundk-design-system/
  design-system.md            # 디자인 시스템 명세 (파운데이션 + 컴포넌트 스펙)
  tokens.json / tokens.css    # 디자인 토큰 (W3C DTCG) + CSS 변수
  i18n-url-hreflang-spec.md   # EN(root) ↔ KO(/kr) URL·hreflang 설계
  kr-build/
    home/                     # 새 메인 홈 (Frame 1 재현, 자립형)
    sub/                      # 서브페이지 소스 (템플릿 + 프래그먼트)
    preview2/                 # 로컬 프리뷰 트리 (/kr/{slug})
    planning/                 # 페이지별 기획서 (콘텐츠 100% 무손실)
```

## 💻 로컬에서 보기

```bash
cd groundk-design-system/kr-build/preview2
python -m http.server 5500
# → http://127.0.0.1:5500/kr/
```

## 📝 비고

- 폰트: Pretendard(본문·국문), Termina(영문 디스플레이, Latin 전용 → 국문 슬롯은 Pretendard 폴백)
- 컬러: primary `#2E3192`, secondary `#2BD9FF`, text `#0F0F0F`
- 레이아웃: 플루이드 vw (데스크톱 1920 기준, 모바일 360 기준 / `max-aspect-ratio: 10/9`)
