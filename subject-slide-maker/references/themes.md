# 교과별 테마 (색 · 폰트 · 모티프)

이 파일은 8개 교과 각각의 **시각 정체성**을 정의한다. 한 슬라이드 덱은 **하나의 교과 테마**를 고른 뒤, 그 교과의 CSS 변수 블록과 폰트 `@import`를 그대로 복사해서 쓴다.

핵심 원칙:

- 모든 색은 **CSS 변수**로 선언한다. 스마트아트 컴포넌트(`smartart.md`)와 교과 전용 틀(`subject-types.md`)은 전부 이 변수만 참조하므로, 변수만 바꾸면 같은 컴포넌트가 교과 색으로 자동 변신한다.
- 폰트는 **무료 웹폰트 CDN**(Google Fonts + Pretendard)만 사용한다. 설치·유료 폰트 금지.
- 교과마다 **제목용 디스플레이 폰트 + 본문용 폰트** 2짝. 한국어 가독성 기본값은 항상 확보.
- 교실 뒷자리 가독성은 교과 불문 공통(큰 글씨, 명확한 대비). 개성은 색·폰트·모티프로 낸다.
- 이모지 금지. AI 클리셰(순수 블랙 + 네온 퍼플/그린) 금지.

---

## 공통 CSS 변수 계약 (모든 테마가 채워야 하는 슬롯)

```css
:root {
  --bg:        /* 라이트 배경 */;
  --bg-dark:   /* 다크(구분/전환) 배경 */;
  --surface:   /* 카드·박스 표면 */;
  --text:      /* 본문 텍스트 */;
  --text-dark: /* 다크 배경 위 텍스트(보통 --bg 계열 밝은색) */;
  --subtext:   /* 캡션·보조 텍스트 */;
  --accent:    /* 메인 강조 (제목 포인트, 핵심 키워드, 1차 노드) */;
  --accent-2:  /* 보조 강조 (대비·현재 표시·2차 노드) */;
  --accent-3:  /* 3차/경고·대조 (위기, 반대 항, 강한 포인트) */;
  --line:      /* 구분선·테두리 */;
  --accent-soft: /* 강조색의 연한 배경 틴트 (카드 배경) */;
}
```

각 컴포넌트는 `var(--accent)`처럼만 쓴다. 절대 hex를 직접 박지 않는다.

---

## 1. 과학 (Science) — 실험·탐구

차갑고 명료한 실험실 톤. 데이터·수치는 모노스페이스로 또렷하게.

```css
@import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css');
@import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@500;600&display=swap');
:root {
  --bg:#f6f9fb; --bg-dark:#0f172a; --surface:#ffffff;
  --text:#0f172a; --text-dark:#e2e8f0; --subtext:#475569;
  --accent:#0e7490;      /* 시안-블루 (탐구) */
  --accent-2:#047857;    /* 에메랄드 (생장·양성 결과) */
  --accent-3:#b91c1c;    /* 적색 (위험·음성·대조) */
  --line:#cbd5e1; --accent-soft:#ecfeff;
  --font-display:'Pretendard'; --font-body:'Pretendard'; --font-data:'IBM Plex Mono';
}
```

- **디스플레이/본문**: Pretendard (기하학적·중립적 산세리프)
- **데이터 폰트**: IBM Plex Mono — 수치, 단위, 측정값, 표의 숫자에만
- **모티프**: 옅은 그리드(모눈), 데이터 눈금, 분자 점. 다크 슬라이드는 슬레이트 네이비(#0f172a)

## 2. 국어 (Korean Literature) — 한지·먹

명조의 서정. 종이의 따뜻함과 먹의 깊이.

```css
@import url('https://fonts.googleapis.com/css2?family=Nanum+Myeongjo:wght@700;800&family=Gowun+Batang:wght@400;700&display=swap');
@import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css');
:root {
  --bg:#f7f3ea; --bg-dark:#1a1a17; --surface:#fffdf8;
  --text:#23211c; --text-dark:#f0ebe0; --subtext:#6b6356;
  --accent:#9f1239;      /* 단청 적 (인장·강조) */
  --accent-2:#1f4e5f;    /* 쪽빛·청자 (대조·차분) */
  --accent-3:#92400e;    /* 토색 갈색 (보조) */
  --line:#ddd4c2; --accent-soft:#f3e9e6;
  --font-display:'Nanum Myeongjo'; --font-body:'Gowun Batang'; --font-data:'Pretendard';
}
```

- **디스플레이**: Nanum Myeongjo 800 (제목·작품명)
- **본문**: Gowun Batang (서술·인용·해설)
- **모티프**: 원고지/세로단 느낌, 낙관(인장) 도형, 한지 결. 작품 인용은 다크(먹) 배경

## 3. 일본어 (Japanese) — 전통 일본(朱·墨·和)

일본 폰트(明朝)로 가나·한자를 또렷하게. 주(朱)와 먹의 대비.

```css
@import url('https://fonts.googleapis.com/css2?family=Shippori+Mincho:wght@600;700;800&family=Zen+Kaku+Gothic+New:wght@500;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Gowun+Batang:wght@400;700&display=swap');
:root {
  --bg:#f6f1e7; --bg-dark:#1b1b1b; --surface:#fffaf2;
  --text:#1f1c19; --text-dark:#f2ece0; --subtext:#6f665a;
  --accent:#c1272d;      /* 朱 (버밀리언) */
  --accent-2:#1f3a5f;    /* 藍 (인디고) */
  --accent-3:#b8860b;    /* 金 (골드) */
  --line:#e0d6c4; --accent-soft:#f7e7e3;
  --font-display:'Shippori Mincho'; --font-body:'Shippori Mincho'; --font-jp-gothic:'Zen Kaku Gothic New'; --font-data:'Gowun Batang';
}
```

- **일본어 본문/제목**: Shippori Mincho (정통 明朝)
- **가나 학습·강조 라벨**: Zen Kaku Gothic New (고딕)
- **한국어 해설**: Gowun Batang
- **모티프**: 縦書き(세로쓰기) 인용, 朱 인장 도형, 미닫이(障子) 격자. 회화·인용은 다크(墨) 배경

## 4. 영어 (English) — 클래식 아카데믹(Oxford)

라틴 세리프의 고전미. 네이비 + 버건디.

```css
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;800&family=Lora:ital,wght@0,400;0,600;1,400&display=swap');
@import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css');
@import url('https://fonts.googleapis.com/css2?family=Gowun+Batang:wght@400;700&display=swap');
:root {
  --bg:#fbfaf6; --bg-dark:#14213d; --surface:#ffffff;
  --text:#1c2230; --text-dark:#e8eaf0; --subtext:#5a6172;
  --accent:#1e3a8a;      /* Oxford navy */
  --accent-2:#7f1d1d;    /* burgundy */
  --accent-3:#a16207;    /* antique gold */
  --line:#d8d4c8; --accent-soft:#eef1fb;
  --font-display:'Playfair Display'; --font-body:'Lora'; --font-ko:'Gowun Batang'; --font-data:'Pretendard';
}
```

- **영어 제목**: Playfair Display (디스플레이 세리프)
- **영어 본문/지문**: Lora (이탤릭 지원 — 인용·예문)
- **한국어 해석**: Gowun Batang
- **모티프**: 사전 표제어 스타일, 괘선(ruled line), 고전 액자

## 5. 윤리 (Ethics) — 사색적 철학(보라·회)

차분한 보라와 회색. 여백으로 사유의 공간.

```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Serif+KR:wght@500;700;900&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Gowun+Batang:wght@400;700&display=swap');
@import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css');
:root {
  --bg:#f8f7fb; --bg-dark:#1e1b2e; --surface:#ffffff;
  --text:#221f2e; --text-dark:#e7e3f0; --subtext:#5b5670;
  --accent:#5b21b6;      /* deep violet */
  --accent-2:#475569;    /* slate (대조·이성) */
  --accent-3:#b45309;    /* amber (가치·따뜻함) */
  --line:#dcd7e6; --accent-soft:#efeafb;
  --font-display:'Noto Serif KR'; --font-body:'Gowun Batang'; --font-data:'Pretendard';
}
```

- **디스플레이**: Noto Serif KR 900 (사상·개념 제목)
- **본문**: Gowun Batang (서술·사유)
- **모티프**: 저울(균형), 넓은 여백, 사상가 흉상 자리. 딜레마는 다크 배경

## 6. 기술 (Technology) — 엔지니어링(그레이·주황)

산업·도면 톤. 라벨·치수는 모노스페이스.

```css
@import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css');
@import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@500;700&display=swap');
:root {
  --bg:#f4f4f5; --bg-dark:#18181b; --surface:#ffffff;
  --text:#18181b; --text-dark:#e4e4e7; --subtext:#52525b;
  --accent:#ea580c;      /* industrial orange */
  --accent-2:#0891b2;    /* steel cyan */
  --accent-3:#dc2626;    /* hazard red (안전·경고) */
  --line:#d4d4d8; --accent-soft:#fff1ea;
  --font-display:'Pretendard'; --font-body:'Pretendard'; --font-data:'JetBrains Mono';
}
```

- **디스플레이/본문**: Pretendard (강한 800)
- **라벨·치수·부품번호**: JetBrains Mono
- **모티프**: 청사진 그리드, 톱니(기어), 안전 경고 줄무늬(빗금). 다크는 zinc-900

## 7. 진로 (Career) — 성장·진취(그린·오렌지)

밝고 따뜻한 성장 톤. 앞으로 나아가는 길.

```css
@import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css');
@import url('https://fonts.googleapis.com/css2?family=Gowun+Dodum&display=swap');
:root {
  --bg:#f5fbf7; --bg-dark:#0f3a2e; --surface:#ffffff;
  --text:#13261d; --text-dark:#e3f4ea; --subtext:#4a6157;
  --accent:#16a34a;      /* growth green */
  --accent-2:#f59e0b;    /* warm orange (기회·에너지) */
  --accent-3:#2563eb;    /* blue (신뢰·계획) */
  --line:#cfe7d8; --accent-soft:#e8f7ee;
  --font-display:'Pretendard'; --font-body:'Gowun Dodum'; --font-data:'Pretendard';
}
```

- **디스플레이**: Pretendard 800 (밝고 둥근 인상)
- **본문**: Gowun Dodum (부드러운 고딕 — 친근함)
- **모티프**: 로드맵 경로, 위로 향하는 화살표, 밝은 카드. 다크는 깊은 숲 그린

## 8. 사서 (Library / Information) — 도서관(우드·그린)

양피지와 책등의 고전미. 분류·정보의 질서.

```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Serif+KR:wght@500;700;900&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Gowun+Batang:wght@400;700&display=swap');
@import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css');
:root {
  --bg:#f8f5ee; --bg-dark:#1f2a24; --surface:#fffdf7;
  --text:#23231d; --text-dark:#ebe7da; --subtext:#665f52;
  --accent:#15803d;      /* forest green */
  --accent-2:#92400e;    /* wood brown */
  --accent-3:#a16207;    /* gold label */
  --line:#ddd5c4; --accent-soft:#e9f1e7;
  --font-display:'Noto Serif KR'; --font-body:'Gowun Batang'; --font-data:'Pretendard';
}
```

- **디스플레이**: Noto Serif KR (분류·표제)
- **본문**: Gowun Batang (안내·해설)
- **라벨/분류번호**: Pretendard (KDC 번호 태그)
- **모티프**: 책등(spine) 줄, 분류 라벨 태그, 카드목록 괘선. 다크는 깊은 녹회색

---

## 테마 빠른 표

| 교과 | 메인색 | 보조색 | 대조/경고 | 디스플레이 폰트 | 본문 폰트 | 모티프 |
|------|--------|--------|-----------|----------------|-----------|--------|
| 과학 | 시안블루 #0e7490 | 에메랄드 #047857 | 적 #b91c1c | Pretendard | Pretendard (+IBM Plex Mono) | 모눈·데이터 눈금 |
| 국어 | 단청적 #9f1239 | 쪽빛 #1f4e5f | 토갈 #92400e | Nanum Myeongjo | Gowun Batang | 원고지·낙관·한지 |
| 일본어 | 朱 #c1272d | 藍 #1f3a5f | 金 #b8860b | Shippori Mincho | Shippori Mincho | 세로쓰기·인장·격자 |
| 영어 | 네이비 #1e3a8a | 버건디 #7f1d1d | 골드 #a16207 | Playfair Display | Lora (+Gowun Batang) | 사전·괘선·액자 |
| 윤리 | 보라 #5b21b6 | 슬레이트 #475569 | 앰버 #b45309 | Noto Serif KR | Gowun Batang | 저울·여백 |
| 기술 | 주황 #ea580c | 스틸시안 #0891b2 | 경고적 #dc2626 | Pretendard | Pretendard (+JetBrains Mono) | 청사진·기어·빗금 |
| 진로 | 그린 #16a34a | 오렌지 #f59e0b | 블루 #2563eb | Pretendard | Gowun Dodum | 로드맵·상승화살 |
| 사서 | 포레스트 #15803d | 우드 #92400e | 골드 #a16207 | Noto Serif KR | Gowun Batang | 책등·분류태그 |

---

## 다크 슬라이드 사용 규칙 (교과 공통)

각 교과의 `--bg-dark`는 **소단원 전환**과 **그 교과의 핵심 자료 한 장**에 쓴다.

- 과학: 우주·미시세계·강조 데이터
- 국어: 작품 원문 인용
- 일본어: 회화 장면·고전 인용
- 영어: 명문장(quote)·핵심 지문
- 윤리: 딜레마 제시
- 기술: 시스템 전체 조감
- 진로: 비전·목표 선언
- 사서: 핵심 분류 체계 개관

다크 배경에서는 텍스트를 `var(--text-dark)`, 강조는 각 교과 메인색을 한 톤 밝게 쓴다.
