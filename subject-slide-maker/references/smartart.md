# 스마트아트 컴포넌트 라이브러리 (순수 CSS)

PPT의 SmartArt를 **순수 CSS 컴포넌트**로 옮긴 것. 외부 라이브러리·SVG 라이브러리 없이 div/CSS만 쓴다.

## 사용 규칙

- 모든 컴포넌트는 **`themes.md`의 CSS 변수만** 참조한다(`var(--accent)` 등). hex 직박기 금지 → 교과 테마만 바꾸면 같은 컴포넌트가 그 교과 색으로 자동 변신.
- 같은 레벨 항목(단계·노드·층)은 **프래그먼트로 순차 등장**시킨다.
- **동심원(겹치는 여러 원) 금지.** 사이클은 노드를 링 위에 배치(단일 트랙선만 허용), 벤다이어그램은 `mix-blend-mode`로 안전 구현.
- 원·정사각형 등 **비율이 중요한 요소는 한 단위(vh)로만** 크기 지정. vw/vh 혼용 금지.
- 텍스트는 `word-break: keep-all`(전역) 전제.

이 라이브러리는 PPT SmartArt 8계열 + 강의용 추가 3종을 담는다:

1. 프로세스(Process) · 2. 사이클(Cycle) · 3. 계층/조직도(Hierarchy) · 4. 피라미드(Pyramid) · 5. 벤다이어그램(Venn) · 6. 매트릭스(Matrix 2×2) · 7. 퍼널/깔때기(Funnel) · 8. 허브-스포크(Hub & Spoke) · (+) 타임라인 · 비교 · 막대그래프

---

## 0. 공통 베이스 CSS

모든 덱에 한 번 넣는다. 컴포넌트들이 공유한다.

```css
* { word-break: keep-all; overflow-wrap: break-word; box-sizing: border-box; }
.sa-node, .sa-card, .sa-chip {
  background: var(--surface);
  border: 2px solid var(--line);
  border-radius: 14px;
  color: var(--text);
  font-family: var(--font-display);
}
.sa-title { font-family: var(--font-display); font-weight: 800; color: var(--text); }
.sa-cap   { font-family: var(--font-body); color: var(--subtext); }
/* 프래그먼트(빌드) — opacity만 애니메이션한다.
   주의: 사이클·허브-스포크 노드는 transform(rotate/translate)으로 위치를 잡으므로,
   .fragment에 transform을 주면 그 위치 transform을 덮어써 노드가 중앙에 겹쳐 사라진다.
   그래서 슬라이드업(translateY) 모션을 쓰지 않고 opacity만 전환한다. */
.fragment { opacity: 0; transition: opacity .4s ease; }
.fragment.visible { opacity: 1; }
```

---

## 1. 프로세스 (Process) — 단계 흐름

"A 다음 B 다음 C", "공정/절차/단계"에 쓴다. 가로 셰브론이 기본.

```html
<div class="sa-process">
  <div class="sa-step fragment"><span class="sa-step-no">1</span><div class="sa-step-t">자료 수집</div><p class="sa-cap">교과서·사료</p></div>
  <div class="sa-step fragment"><span class="sa-step-no">2</span><div class="sa-step-t">분석</div><p class="sa-cap">쪼개고 분류</p></div>
  <div class="sa-step fragment"><span class="sa-step-no">3</span><div class="sa-step-t">재구성</div><p class="sa-cap">시각화</p></div>
</div>
```

```css
.sa-process { display: flex; align-items: stretch; gap: 0; width: 88vw; }
.sa-step {
  position: relative; flex: 1; padding: 3vh 3vw 3vh 4vw;
  background: var(--accent-soft); border: none;
  /* 셰브론(화살표) 모양: 오른쪽 뾰족, 왼쪽 패임 */
  clip-path: polygon(0 0, calc(100% - 1.6vw) 0, 100% 50%, calc(100% - 1.6vw) 100%, 0 100%, 1.6vw 50%);
  margin-right: -1.2vw;
}
.sa-step:first-child { clip-path: polygon(0 0, calc(100% - 1.6vw) 0, 100% 50%, calc(100% - 1.6vw) 100%, 0 100%); }
.sa-step:nth-child(2n) { background: color-mix(in srgb, var(--accent) 14%, var(--surface)); }
.sa-step-no {
  display:inline-flex; align-items:center; justify-content:center;
  width: 4.2vh; height: 4.2vh; border-radius: 50%;
  background: var(--accent); color:#fff; font-family: var(--font-display); font-weight:800; font-size: 2.2vh;
}
.sa-step-t { font-family: var(--font-display); font-weight: 800; font-size: 2.6vh; color: var(--text); margin-top: 1.2vh; }
.sa-step .sa-cap { font-size: 1.8vh; margin-top: .4vh; }
```

세로 변형: `.sa-process` 를 `flex-direction:column`, 셰브론을 아래 방향(`polygon`을 회전)으로. 단계가 5개↑면 세로 권장.

---

## 2. 사이클 (Cycle) — 순환

"순환·반복·되돌아오는 과정"(물 순환, 탄소 순환, PDCA). 노드를 **하나의 링** 위에 배치한다. 동심원 아님.

```html
<div class="sa-cycle" style="--n:4;">
  <div class="sa-cycle-track"></div>
  <div class="sa-cnode fragment" style="--i:0;"><b>흡수</b></div>
  <div class="sa-cnode fragment" style="--i:1;"><b>전환</b></div>
  <div class="sa-cnode fragment" style="--i:2;"><b>이동</b></div>
  <div class="sa-cnode fragment" style="--i:3;"><b>방출</b></div>
  <div class="sa-cycle-hub">순환</div>
</div>
```

```css
.sa-cycle { position: relative; width: 52vh; height: 52vh; }            /* 정사각: vh 한 단위만 */
.sa-cycle-track {
  position: absolute; inset: 8vh; border-radius: 50%;
  border: 3px dashed var(--line);                                       /* 단일 링(트랙)만 — 허용 */
}
.sa-cnode {
  position: absolute; left: 50%; top: 50%;
  width: 15vh; height: 15vh; margin: -7.5vh 0 0 -7.5vh;
  border-radius: 50%; background: var(--accent-soft); border: 3px solid var(--accent);
  display: flex; align-items: center; justify-content: center; text-align: center;
  /* i번째 노드를 360/n*i 각도에 배치: 회전 → 바깥으로 → 다시 역회전(텍스트 수평 유지) */
  transform: rotate(calc(360deg / var(--n) * var(--i))) translateY(-18vh) rotate(calc(-360deg / var(--n) * var(--i)));
}
.sa-cnode b { font-family: var(--font-display); font-weight: 800; font-size: 2.4vh; color: var(--accent); }
.sa-cnode:nth-child(2n) { border-color: var(--accent-2); background: color-mix(in srgb, var(--accent-2) 12%, var(--surface)); }
.sa-cycle-hub {
  position: absolute; left: 50%; top: 50%; transform: translate(-50%,-50%);
  width: 16vh; height: 16vh; border-radius: 50%;
  background: var(--accent); color:#fff; display:flex; align-items:center; justify-content:center;
  font-family: var(--font-display); font-weight: 800; font-size: 2.6vh;
}
```

`--n`(노드 수)과 각 노드의 `--i`(0부터)만 지정하면 자동 배치. 방향 표시가 필요하면 트랙 위에 `▸`를 같은 `transform` 공식으로 노드 사이 각도(`--i: 0.5, 1.5 …`)에 얹는다.

---

## 3. 계층 / 조직도 (Hierarchy)

상하 관계·분류 체계·조직. CSS 커넥터로 트리를 그린다.

```html
<div class="sa-tree">
  <div class="sa-tree-root sa-node fragment">대단원</div>
  <div class="sa-tree-row">
    <div class="sa-branch fragment"><div class="sa-node">소단원 1</div></div>
    <div class="sa-branch fragment"><div class="sa-node">소단원 2</div></div>
    <div class="sa-branch fragment"><div class="sa-node">소단원 3</div></div>
  </div>
</div>
```

```css
.sa-tree { display: flex; flex-direction: column; align-items: center; }
.sa-tree-root { padding: 2vh 4vw; font-size: 2.8vh; font-weight: 800; background: var(--accent); color:#fff; border:none; }
.sa-tree-row { display: flex; gap: 3vw; margin-top: 5vh; position: relative; }
.sa-tree-row::before {                                    /* 루트에서 내려오는 수직선 */
  content:""; position:absolute; top:-5vh; left:50%; width:3px; height:2.5vh; background: var(--line); transform: translateX(-50%);
}
.sa-branch { position: relative; }
.sa-branch::before {                                      /* 각 가지 위 수직선 */
  content:""; position:absolute; top:-2.5vh; left:50%; width:3px; height:2.5vh; background: var(--line); transform: translateX(-50%);
}
.sa-tree-row::after {                                     /* 가지들을 잇는 수평선 */
  content:""; position:absolute; top:-2.5vh; left:12%; right:12%; height:3px; background: var(--line);
}
.sa-tree .sa-node { padding: 1.6vh 2.4vw; font-size: 2.2vh; font-weight: 700; }
```

3단 계층은 `.sa-tree-row` 안에 다시 `.sa-tree`를 중첩.

---

## 4. 피라미드 (Pyramid) — 위계·기초→정점

"기초가 넓고 위로 갈수록 좁아지는" 구조(욕구 위계, 생태 피라미드, 역량 단계). 사다리꼴 층을 쌓는다.

```html
<div class="sa-pyramid">
  <div class="sa-pyr-layer fragment" style="--w:46;"><span>정점</span></div>
  <div class="sa-pyr-layer fragment" style="--w:66;"><span>중간</span></div>
  <div class="sa-pyr-layer fragment" style="--w:88;"><span>기초</span></div>
</div>
```

```css
.sa-pyramid { display: flex; flex-direction: column; align-items: center; gap: 1vh; }
.sa-pyr-layer {
  width: calc(var(--w) * 1vh);              /* 층마다 너비를 vh로 */
  height: 9vh; display: flex; align-items: center; justify-content: center;
  background: var(--accent); color:#fff;
  clip-path: polygon(8% 0, 92% 0, 100% 100%, 0 100%);   /* 사다리꼴 */
}
.sa-pyr-layer:nth-child(1){ background: var(--accent); }
.sa-pyr-layer:nth-child(2){ background: color-mix(in srgb, var(--accent) 70%, var(--surface)); color: var(--text); }
.sa-pyr-layer:nth-child(3){ background: color-mix(in srgb, var(--accent) 40%, var(--surface)); color: var(--text); }
.sa-pyr-layer span { font-family: var(--font-display); font-weight: 800; font-size: 2.4vh; }
```

맨 위 층만 삼각형으로 하려면 첫 층 `clip-path: polygon(50% 0, 100% 100%, 0 100%)`.

---

## 5. 벤다이어그램 (Venn) — 교집합·공통점

겹치는 원의 교집합을 보여준다. **`mix-blend-mode: multiply`** 로 겹친 부분만 진해지게 — 동심원 버그 없음.

```html
<div class="sa-venn">
  <div class="sa-venn-c sa-venn-a"><span>A 특징</span></div>
  <div class="sa-venn-c sa-venn-b"><span>B 특징</span></div>
  <div class="sa-venn-mid">공통점</div>
</div>
```

```css
.sa-venn { position: relative; width: 70vh; height: 40vh; }   /* 가로형: 원 지름은 vh로 통일 */
.sa-venn-c {
  position: absolute; top: 50%; width: 38vh; height: 38vh; margin-top: -19vh;
  border-radius: 50%; display: flex; align-items: center;
  mix-blend-mode: multiply;                                   /* 겹침을 안전하게 표현 */
  font-family: var(--font-display); font-weight: 800; font-size: 2.4vh; color: #fff;
}
.sa-venn-a { left: 0;  background: var(--accent);   justify-content: flex-start; padding-left: 4vh; }
.sa-venn-b { right: 0; background: var(--accent-2); justify-content: flex-end;  padding-right: 4vh; }
.sa-venn-mid {
  position: absolute; left: 50%; top: 50%; transform: translate(-50%,-50%); z-index: 3;
  font-family: var(--font-display); font-weight: 800; font-size: 2.2vh; color: #fff; text-align:center; width: 18vh;
}
```

3원이면 위 1 + 아래 2 삼각 배치, 같은 `mix-blend-mode`. 텍스트가 겹쳐 안 보이면 라벨을 원 바깥 상단으로 빼고 교집합만 가운데에 둔다.

---

## 6. 매트릭스 (Matrix 2×2) — 두 축 분류

두 기준으로 사분면 분류(중요도×긴급도, 비용×효과). 축 라벨 + 4칸.

```html
<div class="sa-matrix">
  <div class="sa-mx-yaxis">높음 ↑ 중요도 ↓ 낮음</div>
  <div class="sa-mx-grid">
    <div class="sa-mx-cell fragment q1"><b>1사분면</b><p class="sa-cap">즉시</p></div>
    <div class="sa-mx-cell fragment q2"><b>2사분면</b><p class="sa-cap">계획</p></div>
    <div class="sa-mx-cell fragment q3"><b>3사분면</b><p class="sa-cap">위임</p></div>
    <div class="sa-mx-cell fragment q4"><b>4사분면</b><p class="sa-cap">제거</p></div>
  </div>
  <div class="sa-mx-xaxis">낮음 ← 긴급도 → 높음</div>
</div>
```

```css
.sa-matrix { display: grid; grid-template-columns: auto 1fr; grid-template-rows: 1fr auto; gap: 1.2vh; width: 70vw; }
.sa-mx-grid { grid-column: 2; grid-row: 1; display: grid; grid-template-columns: 1fr 1fr; grid-template-rows: 1fr 1fr; gap: 1.4vh; height: 56vh; }
.sa-mx-cell { display: flex; flex-direction: column; align-items: center; justify-content: center; border-radius: 14px; border: 2px solid var(--line); background: var(--surface); }
.sa-mx-cell b { font-family: var(--font-display); font-weight: 800; font-size: 2.6vh; color: var(--text); }
.sa-mx-cell.q1 { background: var(--accent-soft); border-color: var(--accent); }
.sa-mx-cell.q3 { background: color-mix(in srgb, var(--accent-2) 10%, var(--surface)); }
.sa-mx-yaxis { grid-column: 1; grid-row: 1; writing-mode: vertical-rl; text-align: center; font-family: var(--font-display); font-weight: 700; color: var(--subtext); }
.sa-mx-xaxis { grid-column: 2; grid-row: 2; text-align: center; font-family: var(--font-display); font-weight: 700; color: var(--subtext); }
```

---

## 7. 퍼널 / 깔때기 (Funnel) — 단계별 좁아짐

"넓게 시작해 좁혀가는" 흐름(후보 → 선별 → 최종, 인식 → 관심 → 구매). 층마다 너비가 줄어든다.

```html
<div class="sa-funnel">
  <div class="sa-fn-layer fragment" style="--w:90;"><span>1단계 · 전체</span></div>
  <div class="sa-fn-layer fragment" style="--w:66;"><span>2단계 · 선별</span></div>
  <div class="sa-fn-layer fragment" style="--w:42;"><span>3단계 · 최종</span></div>
</div>
```

```css
.sa-funnel { display: flex; flex-direction: column; align-items: center; gap: 1.4vh; }
.sa-fn-layer {
  width: calc(var(--w) * 1vh); height: 8.5vh;
  display: flex; align-items: center; justify-content: center;
  background: color-mix(in srgb, var(--accent) calc(var(--w) * 1%), var(--surface));
  color: #fff; border-radius: 8px;
  clip-path: polygon(0 0, 100% 0, 88% 100%, 12% 100%);   /* 아래로 좁아지는 사다리꼴 */
}
.sa-fn-layer span { font-family: var(--font-display); font-weight: 800; font-size: 2.2vh; }
```

피라미드와 차이: 피라미드는 **위가 정점(가치 위계)**, 퍼널은 **아래로 걸러짐(수량 감소)**. 의미에 맞게 고른다.

---

## 8. 허브-스포크 / 방사형 (Hub & Spoke)

"중심 개념에서 뻗어나가는 하위 요소"(핵심어 + 관련 항목). 중앙 노드 + 위성 노드 + 연결선.

```html
<div class="sa-hub" style="--n:5;">
  <div class="sa-hub-center">핵심 개념</div>
  <div class="sa-spoke fragment" style="--i:0;"><span>요소 1</span></div>
  <div class="sa-spoke fragment" style="--i:1;"><span>요소 2</span></div>
  <div class="sa-spoke fragment" style="--i:2;"><span>요소 3</span></div>
  <div class="sa-spoke fragment" style="--i:3;"><span>요소 4</span></div>
  <div class="sa-spoke fragment" style="--i:4;"><span>요소 5</span></div>
</div>
```

```css
.sa-hub { position: relative; width: 56vh; height: 56vh; }
.sa-hub-center {
  position: absolute; left:50%; top:50%; transform: translate(-50%,-50%); z-index:2;
  width: 17vh; height: 17vh; border-radius: 50%; background: var(--accent); color:#fff;
  display:flex; align-items:center; justify-content:center; text-align:center;
  font-family: var(--font-display); font-weight:800; font-size: 2.4vh;
}
.sa-spoke {
  position: absolute; left:50%; top:50%; width: 14vh; height: 14vh; margin:-7vh 0 0 -7vh;
  border-radius: 50%; background: var(--accent-soft); border: 2px solid var(--accent-2);
  display:flex; align-items:center; justify-content:center; text-align:center;
  transform: rotate(calc(360deg / var(--n) * var(--i))) translateY(-20vh) rotate(calc(-360deg / var(--n) * var(--i)));
}
.sa-spoke span { font-family: var(--font-display); font-weight: 700; font-size: 2vh; color: var(--text); }
/* 연결선은 중앙 원에서 의사요소로 그리기보다, 노드 배경 대비로 충분. 선이 꼭 필요하면 각 스포크에
   ::before로 가는 막대를 두고 같은 회전각으로 안쪽(translateY 양수)으로 깐다. */
```

사이클과 차이: 사이클은 **노드끼리 순서로 이어짐(화살표)**, 허브-스포크는 **중심-위성(방사)** 관계. 순서가 없으면 허브.

---

## (+) 타임라인 (연대기 3행 그리드)

라벨/점·선/설명을 같은 그리드 열에 두어 항상 정렬되게 한다.

```html
<div class="sa-tl" style="grid-template-columns: repeat(3, 1fr);">
  <div class="sa-tl-label">1단계</div><div class="sa-tl-label cur">2단계</div><div class="sa-tl-label">3단계</div>
  <div class="sa-tl-track">
    <div class="sa-tl-line"></div>
    <div class="sa-tl-dot"></div><div class="sa-tl-dot cur"></div><div class="sa-tl-dot"></div>
  </div>
  <div class="sa-tl-desc">설명 A</div><div class="sa-tl-desc">설명 B</div><div class="sa-tl-desc">설명 C</div>
</div>
```

```css
.sa-tl { display: grid; width: 86vw; row-gap: 1.4vh; }
.sa-tl-label { text-align:center; font-family: var(--font-display); font-weight:800; font-size:2.2vh; color: var(--accent); }
.sa-tl-label.cur { color: var(--accent-2); }
.sa-tl-track { grid-column: 1 / -1; display:flex; justify-content: space-around; position: relative; height: 4vh; align-items: center; }
.sa-tl-line { position:absolute; left:0; right:0; top:50%; transform:translateY(-50%); height:3px; background: var(--line); }
.sa-tl-dot { width: 1.9vh; height: 1.9vh; border-radius:50%; background: var(--accent); border: 3px solid var(--bg); z-index:1; }
.sa-tl-dot.cur { width: 2.5vh; height: 2.5vh; background: var(--accent-2); box-shadow: 0 0 0 4px color-mix(in srgb, var(--accent-2) 30%, transparent); }
.sa-tl-desc { text-align:center; font-family: var(--font-body); font-size:1.7vh; color: var(--subtext); }
```

이벤트 7개↑면 2장으로 분할.

## (+) 비교 (2단 대조)

```html
<div class="sa-compare">
  <div class="sa-cmp-col"><h3>A</h3><ul><li class="fragment">항목</li><li class="fragment">항목</li></ul></div>
  <div class="sa-cmp-vs">VS</div>
  <div class="sa-cmp-col alt"><h3>B</h3><ul><li class="fragment">항목</li><li class="fragment">항목</li></ul></div>
</div>
```

```css
.sa-compare { display:flex; align-items:stretch; gap:2vw; width: 82vw; }
.sa-cmp-col { flex:1; background: var(--accent-soft); border-radius:16px; padding: 3vh 2.4vw; }
.sa-cmp-col.alt { background: color-mix(in srgb, var(--accent-2) 12%, var(--surface)); }
.sa-cmp-col h3 { font-family: var(--font-display); font-weight:800; font-size:2.8vh; color: var(--accent); margin:0 0 1.4vh; }
.sa-cmp-col.alt h3 { color: var(--accent-2); }
.sa-cmp-col li { font-family: var(--font-body); font-size:2.1vh; color: var(--text); margin:.8vh 0; list-style: none; }
.sa-cmp-vs { align-self:center; font-family: var(--font-display); font-weight:800; font-size:3vh; color: var(--subtext); }
```

## (+) 막대그래프 (수치)

height를 **vh 인라인**으로. 

```html
<div class="sa-bars">
  <div class="sa-bar-col"><div class="sa-bar" style="height: 9vh;"></div><span class="sa-bar-v">120</span><span class="sa-bar-l">A</span></div>
  <div class="sa-bar-col"><div class="sa-bar alt" style="height: 22vh;"></div><span class="sa-bar-v">300</span><span class="sa-bar-l">B</span></div>
</div>
```

```css
.sa-bars { display:flex; align-items:flex-end; gap: 3vw; height: 40vh; }
.sa-bar-col { display:flex; flex-direction:column; align-items:center; justify-content:flex-end; }
.sa-bar { width: 7vw; background: var(--accent); border-radius: 6px 6px 0 0; }
.sa-bar.alt { background: var(--accent-2); }
.sa-bar-v { font-family: var(--font-data); font-weight:600; font-size:2vh; color: var(--text); margin-top:.8vh; }
.sa-bar-l { font-family: var(--font-display); font-size:1.8vh; color: var(--subtext); }
```

---

## 컴포넌트 고르기 빠른 가이드

| 교과서 서술이 이러면 | 이 컴포넌트 |
|---|---|
| 순서/절차/공정 | 프로세스 |
| 돌고 도는 과정·반복 | 사이클 |
| 분류 체계·상하 조직 | 계층/조직도 |
| 기초→정점 위계 | 피라미드 |
| 둘의 공통점·교집합 | 벤다이어그램 |
| 두 기준 사분면 분류 | 매트릭스 |
| 많이→적게 걸러짐 | 퍼널 |
| 중심어 + 뻗는 요소 | 허브-스포크 |
| 연·월·단계 시간순 | 타임라인 |
| 둘 대조 | 비교 |
| 수치 크기 | 막대그래프 |

"하나의 개념 = 하나의 슬라이드 = 하나의 컴포넌트." 한 화면에 두 컴포넌트 욱여넣지 마라.
