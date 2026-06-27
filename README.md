# jini-skill-pack

개인용 Claude Code 커스텀 스킬 모음입니다.  
직접 만들고 사용하는 스킬들을 `claude-skills/` 디렉토리에 관리합니다.

---

## 스킬 목록

| 스킬 | 파일 | 설명 |
|------|------|------|
| book-comparison | [`claude-skills/book-comparison.skill`](claude-skills/book-comparison.skill) | 비슷한 책 여러 권을 비교해 구매 목적에 맞는 One Pick 추천 |

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

---

## 스킬 파일 구조

`.skill` 파일은 ZIP 아카이브입니다. 내부 구조:

```
book-comparison.skill  (ZIP)
└── book-comparison/
    └── SKILL.md       ← 스킬 정의 (메타데이터 + 실행 지침)
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
