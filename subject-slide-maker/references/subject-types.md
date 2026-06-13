# 교과 전용 슬라이드 틀

`smartart.md`의 공통 컴포넌트로 안 잡히는, **그 교과 교과서에만 나오는 자료 형태**를 담는 틀이다. 모두 `themes.md`의 CSS 변수만 참조한다(교과 테마 자동 적용). 각 교과 데모 덱은 아래 틀 중 2~4개를 반드시 활용한다.

원칙: **교과서의 모든 요소(본문·날개·사료·탐구·캡션·각주·용어)를 빠짐없이** 이 틀들에 흡수시킨다. 본문만 옮기고 나머지를 버리지 않는다.

---

## 과학 (Science)

### 실험 과정도 (가설 → 방법 → 결과 → 결론)
프로세스 컴포넌트를 4단계로 쓰되 각 단계에 변인/측정을 명시.
```html
<div class="sci-exp">
  <div class="sci-exp-step fragment"><span class="tag">가설</span><p>빛이 강할수록 광합성량 증가</p></div>
  <div class="sci-exp-step fragment"><span class="tag">방법</span><p>광도 단계별 기포 수 측정</p></div>
  <div class="sci-exp-step fragment"><span class="tag">결과</span><p>광도↑ → 기포 수↑</p></div>
  <div class="sci-exp-step fragment"><span class="tag">결론</span><p>광도와 광합성량은 비례</p></div>
</div>
```
```css
.sci-exp { display:flex; gap:1.2vw; width:88vw; }
.sci-exp-step { flex:1; background:var(--surface); border:2px solid var(--line); border-left:6px solid var(--accent); border-radius:12px; padding:2.4vh 1.4vw; }
.sci-exp-step .tag { font-family:var(--font-display); font-weight:800; font-size:1.8vh; color:#fff; background:var(--accent); padding:.4vh 1vw; border-radius:6px; }
.sci-exp-step:nth-child(3){ border-left-color:var(--accent-2); } .sci-exp-step:nth-child(3) .tag{ background:var(--accent-2); }
.sci-exp-step p { font-family:var(--font-body); font-size:2.1vh; color:var(--text); margin-top:1.2vh; }
```

### 변인 통제 표
```html
<div class="sci-vars">
  <div class="vcell"><h4>조작 변인</h4><p>빛의 세기</p></div>
  <div class="vcell"><h4>통제 변인</h4><p>온도 · CO₂ · 식물 종</p></div>
  <div class="vcell hl"><h4>종속 변인</h4><p>기포 발생 수</p></div>
</div>
```
`.vcell.hl`은 `background:var(--accent-soft); border-color:var(--accent)`. 숫자·단위는 `font-family:var(--font-data)`.

### 구조 도식 (라벨 콜아웃)
교과서 그림(세포·회로·분자)을 캡쳐해 가운데 두고, 주변에 번호 콜아웃. 이미지가 없으면 CSS 도형 + 콜아웃선.
```html
<div class="sci-diagram">
  <img src="images/cell.png" alt="세포 구조">  <!-- 또는 CSS 도형 -->
  <div class="callout" style="top:18%; left:6%;"><b>①</b> 세포막</div>
  <div class="callout" style="bottom:14%; right:8%;"><b>②</b> 엽록체</div>
</div>
```
`.callout`은 `background:var(--surface); border:2px solid var(--accent); border-radius:10px; padding:.8vh 1.2vw`. 데이터 그래프는 `smartart.md`의 막대그래프 사용.

---

## 국어 (Korean Literature)

### 작품 원문 인용 (다크 · 먹)
시·소설 원문은 **다크 배경(`--bg-dark`)** + 세로 여백으로 한 작품을 음미하게.
```html
<section class="slide dark lit-quote">
  <div class="lit-orig">
    죽는 날까지 하늘을 우러러<br>한 점 부끄럼이 없기를,
  </div>
  <div class="lit-meta">윤동주 「서시」 (1941)</div>
</section>
```
`.lit-orig`: `font-family:var(--font-body); font-size:3.4vh; line-height:2; color:var(--text-dark)`. `.lit-meta`: `font-family:var(--font-display); color:var(--accent)`(밝은 단청적). 핵심 시어는 `<b style="color:var(--accent)">`로 강조.

### 문학 분석 카드 (화자 · 주제 · 표현 · 정서)
```html
<div class="lit-analysis">
  <div class="la-card fragment"><h4>화자</h4><p>자기를 성찰하는 '나'</p></div>
  <div class="la-card fragment"><h4>주제</h4><p>부끄럼 없는 삶의 의지</p></div>
  <div class="la-card fragment"><h4>표현</h4><p>대조 · 상징(하늘·바람)</p></div>
  <div class="la-card fragment"><h4>정서</h4><p>고백 · 다짐</p></div>
</div>
```
2×2 그리드. `.la-card h4`는 `var(--accent)` 명조, 본문은 Gowun Batang.

### 어휘·한자 풀이
```html
<div class="lit-word"><div class="lw-head">우러르다</div><div class="lw-mean">위를 향하여 고개를 젖히다 · 공경하다</div><div class="lw-ex">예) 하늘을 우러러 한 점 부끄럼 없이</div></div>
```

---

## 일본어 (Japanese)

### 가나표 (오십음도 일부)
```html
<div class="jp-kana">
  <div class="kcell fragment"><b>あ</b><span>a</span></div>
  <div class="kcell fragment"><b>い</b><span>i</span></div>
  <div class="kcell fragment"><b>う</b><span>u</span></div>
  <!-- ... -->
</div>
```
`.jp-kana{display:grid; grid-template-columns:repeat(5,1fr); gap:1vh;}` `.kcell b`는 Shippori Mincho 5vh `var(--accent)`(朱), `span`은 로마자 Zen Kaku Gothic.

### 회화 말풍선 (다크 가능)
```html
<div class="jp-dialog">
  <div class="bub left fragment"><ruby>初<rt>はじ</rt></ruby>めまして。<p class="ko">처음 뵙겠습니다.</p></div>
  <div class="bub right fragment">どうぞよろしく。<p class="ko">잘 부탁합니다.</p></div>
</div>
```
`.bub`: 말풍선(`border-radius:18px`), left=`var(--accent-soft)`, right=`color-mix(var(--accent-2) 14%)`. 일본어는 Shippori Mincho, `.ko` 해석은 Gowun Batang `var(--subtext)`. `<ruby>`로 요미가나.

### 문형 카드 (예문 + 요미가나 + 해석)
```html
<div class="jp-pattern">
  <div class="jp-form">〜たいです</div>
  <div class="jp-ex"><ruby>日本<rt>にほん</rt></ruby>へ<ruby>行<rt>い</rt></ruby>きたいです。</div>
  <div class="jp-ko">일본에 가고 싶습니다.</div>
</div>
```
`.jp-form`은 朱 배경 칩. 文型을 큰 글씨로.

---

## 영어 (English)

### 어휘 카드 (word · 뜻 · 예문)
```html
<div class="en-vocab">
  <div class="ev-card fragment"><div class="ev-word">resilient</div><div class="ev-pos">adj.</div><div class="ev-mean">회복력 있는</div><div class="ev-ex">She is <i>resilient</i> in hard times.</div></div>
</div>
```
`.ev-word`는 Playfair Display `var(--accent)`(네이비), `.ev-ex`는 Lora 이탤릭, 뜻은 Gowun Batang.

### 지문 + 해석 (2단)
```html
<div class="en-passage">
  <div class="ep-en">It was the best of times, it was the worst of times.</div>
  <div class="ep-ko">최고의 시절이자 최악의 시절이었다.</div>
</div>
```
영문은 Lora, 한글 해석은 Gowun Batang `var(--subtext)`, 핵심 표현은 `var(--accent-2)`(버건디) 밑줄.

### 문법 구조 분해 (SVOC 색상)
```html
<div class="en-grammar">
  <span class="g-s">She</span> <span class="g-v">gave</span> <span class="g-io">me</span> <span class="g-do">a book</span>.
  <div class="g-legend"><span class="g-s">S</span><span class="g-v">V</span><span class="g-io">IO</span><span class="g-do">DO</span></div>
</div>
```
S=`var(--accent)`, V=`var(--accent-2)`, O=`var(--accent-3)` 등 칩 색으로 문장 성분 구분.

### 대화 (dialogue)
일본어 회화 말풍선과 같은 구조, 영어 톤(네이비/버건디)으로.

---

## 윤리 (Ethics)

### 사상가 카드
```html
<div class="eth-thinker">
  <div class="et-bust">칸</div>            <!-- 이름 첫 글자 원형 -->
  <div class="et-name">칸트</div>
  <div class="et-dates">1724~1804</div>
  <div class="et-core">정언명령 · 인간을 목적으로 대하라</div>
</div>
```
역사 인물 카드와 유사하나 **핵심 명제**를 크게. 흉상 자리는 `var(--accent)`(보라) 원.

### 딜레마 저울 (다크)
양자택일을 저울로. 동심원 금지 → 저울대 + 두 접시.
```html
<section class="slide dark eth-dilemma">
  <div class="ed-beam"></div>
  <div class="ed-pan left fragment"><b>의무</b><p>약속은 지켜야</p></div>
  <div class="ed-pan right fragment"><b>결과</b><p>더 많은 생명</p></div>
  <div class="ed-q">무엇이 옳은가?</div>
</section>
```
`.ed-beam`은 가로 막대(`var(--accent)`), 두 `.ed-pan`은 양쪽 카드. 좌=의무론 톤, 우=결과론 톤. 매트릭스·비교로 사상 대조도 가능.

---

## 기술 (Technology)

### 공정 흐름 (입력 → 가공 → 출력)
프로세스 셰브론을 쓰되 단계마다 도구/조건 라벨(모노스페이스 `var(--font-data)`).

### 부품 분해 (콜아웃)
과학 구조 도식과 같은 콜아웃 틀, 기술 톤. 부품번호는 JetBrains Mono.
```html
<div class="tech-explode">
  <img src="images/device.png" alt="장치">
  <div class="callout"><b>P-01</b> 모터</div>
  <div class="callout"><b>P-02</b> 기어</div>
</div>
```

### 안전수칙 (경고 줄무늬)
```html
<div class="tech-safety">
  <div class="ts-bar"></div>
  <ul>
    <li class="fragment"><span class="warn">!</span> 전원 차단 후 점검</li>
    <li class="fragment"><span class="warn">!</span> 보호장구 착용</li>
  </ul>
</div>
```
`.ts-bar`는 빗금 경고 줄무늬: `background:repeating-linear-gradient(45deg,var(--accent-3) 0 2vh,#1f1f1f 2vh 4vh)`. `.warn`은 `var(--accent-3)` 원형.

---

## 진로 (Career)

### 직업 카드 (하는 일 · 역량 · 전망)
```html
<div class="car-job">
  <div class="cj-title">데이터 분석가</div>
  <div class="cj-row"><b>하는 일</b><p>데이터로 의사결정 지원</p></div>
  <div class="cj-row"><b>필요 역량</b><p>통계 · 프로그래밍 · 커뮤니케이션</p></div>
  <div class="cj-row"><b>전망</b><p class="up">▲ 성장</p></div>
</div>
```
`.cj-title`은 `var(--accent)`(그린), `.up`은 오렌지 상승. 

### 로드맵 (단계별 목표)
타임라인 컴포넌트를 진로 톤으로, 각 점에 '학년/시기 + 목표'.

### 의사결정 매트릭스
매트릭스(2×2) 또는 가치 기준 표로 진로 선택 비교.

---

## 사서 (Library / Information)

### 분류 트리 (KDC)
계층/조직도 컴포넌트로 KDC 0~9 대분류 → 중분류.
```html
<div class="lib-kdc">
  <div class="lk-root">KDC</div>
  <div class="lk-row">
    <div class="lk-node fragment"><b>0</b> 총류</div>
    <div class="lk-node fragment"><b>8</b> 문학</div>
    <div class="lk-node fragment"><b>9</b> 역사</div>
  </div>
</div>
```
분류번호 태그는 `var(--accent-3)`(골드) 라벨, Pretendard.

### 정보활용 절차 (Big6 등)
프로세스 6단계: 과제정의 → 정보탐색 → 소재파악 → 활용 → 종합 → 평가.

### 출처·인용 카드
```html
<div class="lib-cite"><div class="lc-type">단행본</div><div class="lc-body">저자(연도). <i>서명</i>. 출판사.</div></div>
```
책등(spine) 모티프: 카드 왼쪽에 `border-left:8px solid var(--accent)`.

---

## 역사 (History) — 한국사·동양사·서양사 공용

연대기는 `smartart.md`의 **타임라인**, 시기·세력 대조는 **비교**, 인구·생산량 수치는 **막대그래프**를 그대로 쓴다. 아래는 역사 교과서에만 나오는 전용 틀이다. (역사 테마는 `themes.md` 9번.)

### 사료 원문 인용 (다크 · 양피지)
원문 사료가 나오면 **슬라이드 배경을 다크(`--bg-dark`)로 전환**한다 — 오래된 문서를 꺼내 보는 분위기. 사진·지도 자료 슬라이드는 라이트 배경 그대로 둔다.
```html
<section class="slide dark his-source">
  <div class="hs-orig">"널리 인간을 이롭게 하라(弘益人間)"</div>
  <div class="hs-trans">널리 인간 세상을 이롭게 한다는 건국 이념</div>
  <div class="hs-meta">— 『삼국유사』 고조선조</div>
</section>
```
`.hs-orig`: `font-family:var(--font-body); font-size:3.4vh; line-height:1.9; color:var(--text-dark)` (큰따옴표와 함께). `.hs-trans`: Gowun Batang, `var(--accent)`를 한 톤 밝게(예: `#d97706`), 본문 크기. `.hs-meta`: Pretendard, 캡션 크기, `var(--subtext)`.

### 인물 카드 (이름 · 생몰년 · 업적)
```html
<div class="his-people">
  <div class="hp-card fragment">
    <div class="hp-initial">세</div>
    <div class="hp-name">세종</div>
    <div class="hp-dates">1397~1450</div>
    <div class="hp-desc">훈민정음 창제 · 과학기술 진흥</div>
  </div>
  <!-- 2~4명: 가로 그리드, 프래그먼트 순차 등장 -->
</div>
```
`.hp-initial`은 이름 첫 글자 원형 아바타: `background:var(--accent); color:#fff; border-radius:50%`. `.hp-name`은 Pretendard 800, `.hp-dates`는 `var(--font-data) var(--subtext)`, `.hp-desc`는 Gowun Batang. 윤리 사상가 카드와 같은 계열이되 **핵심 업적**을 중심에 둔다.

### 인과관계도 (원인 → 과정 → 결과)
가로 3단 flexbox + 화살표(→). 각 단계는 프래그먼트로 순차 공개. **원인=`--accent-3`(적) 톤, 과정=중립, 결과=`--accent-2`(녹) 톤**으로 흐름을 색으로 읽힌다.
```html
<div class="his-cause">
  <div class="hc-step fragment cause"><span class="tag">원인</span><p>세도정치 · 삼정 문란</p></div>
  <div class="hc-arrow">→</div>
  <div class="hc-step fragment"><span class="tag">전개</span><p>농민 봉기 확산</p></div>
  <div class="hc-arrow">→</div>
  <div class="hc-step fragment result"><span class="tag">결과</span><p>갑오개혁의 배경</p></div>
</div>
```
`.hc-step`은 `background:var(--surface); border:2px solid var(--line)` 카드. `.hc-step.cause`는 `border-left:6px solid var(--accent-3)`, `.hc-step.result`는 `border-left:6px solid var(--accent-2)`. `.hc-arrow`는 `var(--accent)` 큰 글씨. 동심원 금지 원칙(`SKILL.md`)을 따른다.

---

## 사회 (Social Studies) — 통합사회·정치·경제·법·사회문화·지리 공용

개념 분류는 `smartart.md`의 **계층/매트릭스/벤**, 시간 추이·통계는 **막대그래프·타임라인**, 제도·절차는 **프로세스**를 그대로 쓴다. 아래는 사회 교과서에 자주 나오는 전용 틀이다. (사회 테마는 `themes.md` 10번. 수치는 `var(--font-data)`.)

### 수요·공급 그래프 (균형점)
경제 단원의 X자 교차 그래프. 두 선을 회전 div로 만들고 교차점에 균형점 라벨.
```html
<div class="soc-sd">
  <div class="sd-plot">
    <span class="sd-y">가격</span><span class="sd-x">거래량</span>
    <div class="sd-line demand"></div>   <!-- 수요: 우하향 -->
    <div class="sd-line supply"></div>   <!-- 공급: 우상향 -->
    <div class="sd-eq fragment"><b>E</b> 균형점</div>
  </div>
  <div class="sd-legend"><span class="lg demand">수요곡선</span><span class="lg supply">공급곡선</span></div>
</div>
```
`.sd-plot`은 정사각 플롯(`width:46vh; height:46vh; border-left:3px solid var(--line); border-bottom:3px solid var(--line)`). `.sd-line`은 `position:absolute; height:3px; width:130%; transform-origin:left`로 깔고, demand는 `rotate(28deg)`+`var(--accent-3)`, supply는 `rotate(-28deg)`+`var(--accent)`. `.sd-eq`는 교차점에 `var(--accent-2)` 점+라벨. 비율 요소이므로 **vh 단위로 통일**(vw 혼용 금지).

### 삼권분립 / 견제와 균형
입법·행정·사법을 삼각 배치, 서로 견제 화살표. 동심원 금지 → 3노드 + 양방향 화살표.
```html
<div class="soc-power">
  <div class="pw-node top fragment"><b>입법부</b><p>국회 · 법률 제정</p></div>
  <div class="pw-node left fragment"><b>행정부</b><p>정부 · 법 집행</p></div>
  <div class="pw-node right fragment"><b>사법부</b><p>법원 · 법 적용</p></div>
  <div class="pw-center">견제와 균형</div>
</div>
```
`.pw-node`는 `background:var(--surface); border:2px solid var(--accent); border-radius:14px`. 노드 사이 견제 관계는 `↔` 라벨(예: "국정감사", "위헌법률심판", "탄핵")로 표기. 삼권을 각각 `--accent`/`--accent-2`/`--accent-3` 테두리로 구분해도 좋다.

### 인구 피라미드 (좌우 양방향 막대)
`smartart.md`의 피라미드(위계)와 **다르다** — 연령대별 좌(남)·우(여) 막대.
```html
<div class="soc-poppyr">
  <div class="pp-row"><span class="pp-bar m" style="width:22%"></span><span class="pp-age">65+</span><span class="pp-bar f" style="width:28%"></span></div>
  <div class="pp-row"><span class="pp-bar m" style="width:38%"></span><span class="pp-age">15~64</span><span class="pp-bar f" style="width:37%"></span></div>
  <div class="pp-row"><span class="pp-bar m" style="width:16%"></span><span class="pp-age">0~14</span><span class="pp-bar f" style="width:15%"></span></div>
</div>
```
`.pp-row`는 `display:grid; grid-template-columns:1fr auto 1fr; align-items:center`. `.pp-bar.m`은 `justify-self:end; background:var(--accent)`, `.pp-bar.f`는 `background:var(--accent-2)`. `.pp-age`는 가운데 `var(--font-data)` 라벨. 막대 너비(%)는 inline으로.

### 통계 지표 카드 (지표 · 수치 · 출처)
```html
<div class="soc-stat">
  <div class="st-card fragment"><div class="st-num">0.92</div><div class="st-label">지니계수 추이</div><div class="st-src">통계청, 2023</div></div>
  <div class="st-card fragment up"><div class="st-num">3.6<small>%</small></div><div class="st-label">경제성장률</div><div class="st-src">한국은행</div></div>
</div>
```
`.st-num`은 큰 `var(--font-data)` `var(--accent)`. `.st-card.up`은 `var(--accent-2)` 상승, 하락 사례는 `.down`+`var(--accent-3)`. 헌법 조문·판례 인용은 `var(--font-quote)`(Gowun Batang)로, 쟁점·갈등 사례는 다크 슬라이드로.

---

## 교과 전용 틀 요약

| 교과 | 전용 틀 |
|------|---------|
| 과학 | 실험 과정도 · 변인 통제표 · 구조 도식(콜아웃) |
| 국어 | 작품 원문 인용(다크) · 문학 분석 카드 · 어휘/한자 풀이 |
| 일본어 | 가나표 · 회화 말풍선(요미가나) · 문형 카드 |
| 영어 | 어휘 카드 · 지문+해석 · 문법 구조 분해 · 대화 |
| 윤리 | 사상가 카드 · 딜레마 저울(다크) · 사상 비교 |
| 기술 | 공정 흐름 · 부품 분해(콜아웃) · 안전수칙(경고 줄무늬) |
| 진로 | 직업 카드 · 로드맵 · 의사결정 매트릭스 |
| 사서 | 분류 트리(KDC) · 정보활용 절차 · 출처/인용 카드 |
| 역사 | 사료 원문 인용(다크) · 인물 카드 · 인과관계도 (+ 타임라인·비교·막대그래프) |
| 사회 | 수요·공급 그래프 · 삼권분립 도식 · 인구 피라미드 · 통계 지표 카드 (+ 계층·매트릭스·막대그래프) |
