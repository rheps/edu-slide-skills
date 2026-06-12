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
