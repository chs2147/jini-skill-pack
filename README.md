# jini-skill-pack

개인용 Claude Code 커스텀 스킬 모음입니다.  
직접 만들고 사용하는 스킬들을 `claude-skills/` 디렉토리에 관리합니다.

---

## 스킬 목록

| 스킬 | 파일 | 설명 |
|------|------|------|
| book-comparison | [`claude-skills/book-comparison.skill`](claude-skills/book-comparison.skill) | 비슷한 책 여러 권을 비교해 구매 목적에 맞는 One Pick 추천 |
| travel-guidebook | [`claude-skills/travel-guidebook.skill`](claude-skills/travel-guidebook.skill) | 여행 일정을 일자별 탭·동선 지도·바우처 카드로 구성한 멀티챕터 HTML 가이드북 생성 |

---

## 스킬 설치 방법

### 1. 이 저장소 클론

```bash
git clone https://github.com/chs2147/jini-skill-pack.git
```

### 2. Claude Code에 스킬 추가

`.skill` 파일을 Claude Code 프로젝트의 스킬 디렉토리에 추가하거나,
Claude Code 데스크탑 앱에서 **Settings → Skills → Import** 로 불러옵니다.

```bash
# 예시: 특정 프로젝트에 스킬 설치
cp claude-skills/book-comparison.skill ~/.claude/skills/
```

또는 Claude Code CLI에서 직접 경로를 지정해 로드할 수 있습니다.

---

## 스킬 상세

### book-comparison

서점/온라인서점에서 비슷한 책들 중 어떤 책을 살지 고민될 때 사용합니다.

**트리거 상황**
- 책 제목을 여러 개 나열하며 "비교해줘", "어떤 책 사야 할지" 같은 말을 할 때
- 서점 매대나 책 표지 사진을 올렸을 때

**스킬이 하는 일**
1. 비교 대상 도서 확정 (텍스트 또는 사진 인식)
2. 구매 목적 확인 (실무 적용 / 취미 / 깊은 학습 등)
3. 각 책의 출판일 · 저자 · 난이도 · 차별점 · 부가자료 · 가격을 웹 검색으로 조사
4. 비교표(항목=행, 도서=열) 작성 + **One Pick** 추천
5. 비교 대상이 3권 이상이면 엑셀 파일도 함께 제공

### travel-guidebook

여행 일정 정보를 공유 가능한 단일 HTML 파일로 만들어줍니다.

**트리거 상황**
- "여행 가이드북 만들어줘", "이 일정 정리해서 파일로 만들어줘" 같이 말할 때
- 항공권·호텔 예약 확정 정보와 일자별 일정을 한 파일로 모으고 싶을 때
- 기존 가이드북에 예약 변경(호텔·항공 변경, 일정 추가)을 반영할 때

**스킬이 하는 일**
1. 여행 일정 · 목적지 · 인원 · 예산 · 숙박/항공 예약 여부를 한 번에 확인
2. 식당·장소 정보를 웹 검색으로 실제 검증 (영업시간·휴무 지어내지 않음)
3. 아래 구조의 멀티챕터 HTML 파일 생성:
   - **일정 탭** — 일자별 탭 네비게이션
   - **동선 지도** — 일자별 개략도(스키매틱) + 전체 동선 한눈에 보기
   - **미식 챕터** — 추천 식당·카페 카드
   - **바우처 챕터** — 호텔/항공권 예약 확인 카드
   - **공항 이동 챕터** — 공항 접근 수단 정리
4. 목적지 분위기에 맞춰 매번 새로운 시각 테마 디자인 (템플릿 재탕 없음)

---

## 스킬 파일 구조

`.skill` 파일은 ZIP 아카이브입니다. 내부 구조:

```
book-comparison.skill  (ZIP)
└── book-comparison/
    └── SKILL.md            ← 스킬 정의 (메타데이터 + 실행 지침)

travel-guidebook.skill  (ZIP)
└── travel-guidebook/
    ├── SKILL.md            ← 스킬 정의
    └── scripts/
        └── compute_route_map.py   ← 동선 지도 계산 헬퍼 스크립트
```

`SKILL.md` 상단의 frontmatter에 `name`과 `description`을 정의하면
Claude Code가 해당 스킬을 인식하고 적절한 상황에 자동으로 트리거합니다.

---

## 새 스킬 추가

새 스킬을 만들어 이 팩에 추가하려면:

1. `<스킬명>/SKILL.md` 파일 작성
2. ZIP으로 압축해 `<스킬명>.skill` 생성
3. `claude-skills/` 디렉토리에 배치
4. 이 README의 스킬 목록 업데이트

```bash
# .skill 파일 생성 예시
zip -r my-skill.skill my-skill/
mv my-skill.skill claude-skills/
```
