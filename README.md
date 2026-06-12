# edu-slide-skills

중·고등학교 **교과 수업용 웹 슬라이드**를 만드는 [Claude Code](https://claude.com/claude-code) 스킬 모음입니다.
교과서 내용(PDF·텍스트)을 받아, 단원 구조에 맞춰 **교과별 전용 스타일**의 한 화면 = 한 메시지 슬라이드로 재구성합니다.

## 들어 있는 스킬

### `subject-slide-maker`
8개 교과를 지원합니다 — **기술 · 윤리 · 영어 · 국어 · 일본어 · 과학 · 진로 · 사서**.

- 교과마다 **색·폰트·모티프가 전부 다릅니다.** (예: 과학=실험 블루/시안, 국어=한지·먹+명조, 일본어=朱·墨+일본 명조, 영어=클래식 네이비+세리프, 윤리=보라+세리프, 기술=주황+모노스페이스, 진로=성장 그린, 사서=도서관 그린+우드)
- PPT **SmartArt식 순수 CSS 컴포넌트** 11종: 프로세스 · 사이클 · 계층/조직도 · 피라미드 · 벤다이어그램 · 매트릭스 · 퍼널 · 허브-스포크 · 타임라인 · 비교 · 막대그래프. 교과 테마 색이 자동 적용됩니다.
- 교과 **전용 슬라이드 틀**: 과학 실험 과정도, 국어 작품 인용·문학 분석, 일본어 가나표·회화(요미가나), 영어 어휘 카드·SVOC 분해, 윤리 사상가 카드·딜레마 저울, 기술 공정 흐름·안전수칙, 진로 직업 카드·로드맵, 사서 KDC 분류 트리·정보활용 절차 등.
- 교과서 PDF에서 텍스트·이미지를 자동 추출하는 `scripts/extract_pdf.py` 포함.

`demos/` 폴더에 8교과 데모 덱이 들어 있습니다 — 브라우저로 열어 키보드(→ ←)로 넘겨 보세요.

> 역사(한국사·동양사·서양사)는 별도 스킬 `history-slide-maker`를 사용하세요.

## 설치 방법

이 스킬들은 개인 스킬 폴더(`~/.claude/skills/`)에 두면 Claude Code가 자동으로 인식합니다.

### macOS / Linux

```bash
git clone https://github.com/rheps/edu-slide-skills.git
cp -r edu-slide-skills/subject-slide-maker ~/.claude/skills/
```

### Windows (PowerShell)

```powershell
git clone https://github.com/rheps/edu-slide-skills.git
Copy-Item -Recurse edu-slide-skills\subject-slide-maker $env:USERPROFILE\.claude\skills\
```

설치 후 **Claude Code를 다시 시작**하면 스킬이 로드됩니다.

### 업데이트

```bash
cd edu-slide-skills && git pull
cp -r subject-slide-maker ~/.claude/skills/       # 다시 복사 (Windows는 위 Copy-Item)
```

## 사용 방법

설치 후, Claude Code에서 교과 수업 슬라이드를 요청하면 스킬이 자동으로 동작합니다.

> 예) "과학 교과서 이 PDF로 단원 슬라이드 만들어줘", "윤리 수업자료 슬라이드 만들어줘", "국어 진달래꽃 단원 PT 만들어줘"

교과서 PDF가 있으면 함께 주면 더 좋습니다. 텍스트만 줘도 됩니다.

## 라이선스

[MIT](./LICENSE)
