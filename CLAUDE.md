# Hebron KM Young Adults — 주보 프로젝트 가이드

## 프로젝트 개요
헤브론 KM 청년부의 주간 온라인 주보를 HTML 단일 파일로 제작.
매주 내용을 업데이트하고 Netlify에 드래그앤드롭으로 배포.

---

## 고정 정보 (절대 바꾸지 말 것)
| 항목 | 값 |
|------|-----|
| 장소 | KM 청년부실 |
| 예배 시간 | 매주 주일 1:30 PM |
| 담당 목사 | 신성은 목사 (기본값, 설교자는 매주 바뀔 수 있음) |
| 이메일 | hebronchurch2020@gmail.com |
| 인스타그램 | @hebronkmya (https://www.instagram.com/hebronkmya/) |
| 연간 주제 | "복음의 대상자인 세상을 알자" (2026) |
| 헌금 종류 | 1.주일헌금 및 기타헌금 / 2.십일조 / 3.감사헌금 / 4.절기헌금 |
| 헌금 이메일 형식 | #. 영문이름. KMC (예: 2. First Last. KMC) |
| 헌금 안내 문구 | "헌금은 예배 전에 드리시면 됩니다. (따로 헌금 시간은 없습니다)" |

---

## 매주 바뀌는 내용
- 날짜 (영문, 예: April 26th, 2026 · Sunday)
- 찬양 목록 (세로 나열, `<br>` 사용)
- 대표 기도자
- 설교 제목 + 본문
- 설교 후 찬양
- 청년부 소식 (광고)
- 시편 묵상 날짜 및 편수 (월~금, 5칸 그리드)
- 목장 나눔 질문

---

## 페이지 구조
```
<header class="hero">       # 흰 배경: 날짜(회색) + 제목 + .theme-bar(연간 주제 한 줄)
<div class="main-wrapper">  # 한 컬럼 (최대 600px, 모바일 우선) — 정보 카드는 맨 아래
  <main>
    .card — 예배 순서       # 예배 순서 + 헌금 안내 (카드 맨 아래)
    .card — 청년부 소식     # 광고/공지
    .recruit-card           # 특별 모집 광고 (어두운 배경, 필요시만)
    .card — 목장 나눔       # 나눔 질문 (항상 메인 컬럼에, 사이드바 아님)
  </main>
  <aside class="sidebar">    # 한 컬럼이라 메인 아래에 이어짐
    .card — 정보            # 장소, 예배시간, 목사, 인스타 (이메일 없음)
  </aside>
</div>
<footer>                    # 한 줄만: Hebron KM Young Adults · 헤브론KM 청년부
```

---

## 이메일 규칙 (중요!)
- 이메일은 **절대 `<a href="mailto:...">` 링크로 넣지 말 것** — Cloudflare가 자동으로 난독화시킴
- 항상 plain text로 표시
- 헌금 안내 섹션의 이메일에는 **복사 버튼** 포함:

```html
<div style="display:flex; align-items:center; justify-content:space-between; background:rgba(255,255,255,0.08); border:1px solid rgba(255,255,255,0.15); border-radius:4px; padding:0.4rem 0.6rem; margin-top:0.3rem;">
  <code style="color:#fff; font-size:0.78rem; user-select:all;">hebronchurch2020@gmail.com</code>
  <button onclick="navigator.clipboard.writeText('hebronchurch2020@gmail.com'); this.innerHTML='✓'; this.style.background='#5C8A60'; setTimeout(()=>{ this.innerHTML='복사'; this.style.background='rgba(255,255,255,0.12)'; }, 2000);"
    style="background:rgba(255,255,255,0.12); color:rgba(255,255,255,0.8); border:none; border-radius:3px; padding:0.25rem 0.6rem; font-size:0.7rem; cursor:pointer; flex-shrink:0; margin-left:0.6rem; font-family:'Noto Sans KR',sans-serif;">복사</button>
</div>
```

- 정보 사이드바에는 이메일 항목 없음
- footer에는 이메일 없음 (한 줄 이름만)

---

## UI — 제거된 것들 (다시 넣지 말 것)
- 헤더의 동그란 로고 이미지
- 헤더 아래 말씀 구절 바 (verse bar)
- 오늘의 설교 섹션 (별도 카드)
- 청년부 소식의 태그 버튼들 ("NEW", "모집중", "QT" 등)
- 정보 사이드바의 이메일 항목
- 정보 사이드바의 주보 링크 항목
- 헤더 가운데 십자가 엠블럼
- 헤더의 info-chip (예배 시간 / 장소 / 목사)
- 헤더의 그라데이션 배너, "주보" 알약, 장식 원
- 카드 제목 옆 아이콘 박스 (.card-icon)

---

## 레이아웃 규칙
- **목장 나눔은 메인 컬럼**에 위치 (사이드바 아님) — 페이지 너비와 상관없이 항상 청년부 소식 아래
- 찬양 목록은 `<br>`로 세로 나열 (가로로 · 구분 금지)
- 찬양 제목 입력 시 한국어 맞춤법 및 띄어쓰기를 자동으로 검토하여 올바르게 수정할 것 (사용자가 틀릴 수 있음)
- 특별 광고(찬양팀 모집 등)는 `.recruit-card` (어두운 배경)로 별도 카드
- 정보 섹션 아이템 정렬은 `grid-template-columns: 1.5rem 3rem 1fr` 사용 (flex 아님)

---

## 디자인 (2026-09 리디자인: 깔끔 + 살짝 발랄)
- 주로 **모바일**로 봄 → 모바일 우선, 한 컬럼 (최대 600px)
- 연회색 배경 위 흰색 둥근 카드 (radius 24px, 그림자 없음)
- 헤더: 연한 파란 배경 + 날짜 알약 + "헤브론 청년부 👋" + 흰색 주제 박스
- 카드 제목 앞 아이콘: 남색 선 SVG (`.title-ico`) — 십자가(예배 순서) / 확성기(청년부 소식) / 말풍선(목장 나눔) / 위치 핀(정보). 이모지 사용 안 함
- 번호는 남색 동그라미, `<strong>`은 노란 형광펜
- 포인트 색은 남색(`--accent`) 하나 — 그라데이션·장식 원 금지

```css
--ink: #191F28     /* 제목 */
--body: #4E5968    /* 본문 */
--gray: #8B95A1    /* 보조 텍스트 */
--gap: #F2F4F6     /* 페이지 배경 */
--soft: #F9FAFB    /* 헌금 박스 배경 */
--accent: #3451B2  /* 포인트 남색 */
--navy: #1B2559    /* 이메일 헌금 박스, recruit-card 배경 */
--tint: #EDF2FF    /* 헤더, 설교 행, 묵상 칸 */
--marker: #FFEC99  /* 형광펜 */
```

## 폰트
- Pretendard Variable (jsdelivr CDN) 하나만 사용
- 파일 구성: `index.html` + `style.css` (Netlify에는 두 파일 + 이미지 함께 배포)

---

## 예배 순서 기본 틀
```
01  사도신경 — 다같이
02  찬양 및 경배 — Atom Worship  ← 찬양 목록 세로 나열
03  대표 기도 — [이름]
04  설교 — [제목] / [본문] — [설교자]  ← .hl 클래스로 강조
05  찬양 — [설교 후 찬양]
06  축도 — [설교자]
07  광고 — 임원
    └── 헌금 안내 박스 (카드 내부 하단, <details>로 기본 접힘 — 눌러서 펼침)
```

---

## 시편 묵상 그리드 (qt-grid)
월~금 5칸:
```html
<div class="qt-grid">
  <div class="qt-day">
    <div class="qt-date">4/27 월</div>
    <div class="qt-ref">시편 66편</div>
  </div>
  ...
</div>
```

---

## 특별 광고 카드 (.recruit-card)
찬양팀 모집처럼 긴 내용의 별도 광고는 어두운 배경의 recruit-card로 분리.
청년부 소식 카드에는 "자세한 내용은 아래 모집 안내를 확인해 주세요" 한 줄만.

---

## 배포 방법 (Netlify)
1. `youth_bulletin.html` 수정 완료
2. [netlify.com](https://netlify.com) 로그인
3. Sites 탭 → 하단 드래그앤드롭 영역에 파일 드롭
4. 같은 URL 유지됨 (예: hebronkmya.netlify.app)
5. 도메인 이름 변경: Site settings → Domain management → Edit site name

---

## 파일
```
youth_bulletin.html   # 단일 파일, 매주 덮어쓰기
CLAUDE.md             # 이 파일
```