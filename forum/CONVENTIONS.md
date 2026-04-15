# Forum File Conventions

`forum/` 폴더에 포켓몬 배틀 가이드 JSON을 추가하거나 수정할 때 반드시 지켜야 하는 규약입니다.

## 1. 파일명

형식: `{pokemonId}[-{formKey}].{locale}.json`

- **pokemonId**: PokeAPI 국가도감 번호 (예: `115`, `6`, `952`)
- **formKey**(선택): 기본형이 아닐 때만 하이픈으로 연결
  - 예: `-mega`, `-mega-x`, `-mega-y`
  - 특수 케이스: `6-charizard-mega-x` 처럼 포켓몬명을 포함하는 변형도 존재
- **locale**: `ko` 또는 `en`
- 한 엔트리는 반드시 `ko`/`en` **두 언어 파일을 쌍으로** 생성한다.

예시:
- `115.ko.json` / `115.en.json` — 캥카 기본형
- `115-mega.ko.json` / `115-mega.en.json` — 메가캥카

## 2. JSON 스키마

필드 순서는 아래 순서를 유지한다.

| 필드 | 타입 | 설명 |
|---|---|---|
| `pokemonId` | number | 국가도감 번호 |
| `nameKo` | string | 한글명 |
| `nameEn` | string | 영문 슬러그 (kebab-case, 예: `kangaskhan-mega`) |
| `formKey` | string \| null | 폼 키 (`mega`, `mega-x`, ...) 또는 기본형이면 `null` |
| `types` | string[] | 타입 슬러그 배열 |
| `roles` | string[] | 역할 태그 (`physical-attacker`, `sweeper`, `pivot` 등) |
| `recommendedAbility` | string | 특성 슬러그 |
| `recommendedNature` | string | 성격 슬러그 |
| `recommendedTera` | string[] | 테라스탈 타입 슬러그 배열 |
| `recommendedEv` | object | `{ hp, atk, def, spa, spd, spe }` 노력치 |
| `locale` | `"ko"` \| `"en"` | 파일명 locale과 일치 |
| `title` | string | 언어별 제목 |
| `summary` | string | 한 줄 요약 |
| `strengths` | string[] | 강점 불릿 |
| `weaknesses` | string[] | 약점 불릿 |
| `recommendedMoves` | `{move, reason}[]` | 기술 슬러그 + 설명 |
| `recommendedItems` | `{item, reason}[]` | 아이템 슬러그 + 설명 |
| `bodyMarkdown` | string | 본문 마크다운 |
| `tags` | string[] | 분류 태그 (세대/타입/특성/역할) |
| `updatedAt` | string | ISO8601 (+09:00 KST) |

### 언어 쌍 일관성

다음 필드는 `ko`/`en` 두 파일에서 **완전히 동일**해야 한다:
`pokemonId`, `nameKo`, `nameEn`, `formKey`, `types`, `roles`,
`recommendedAbility`, `recommendedNature`, `recommendedTera`,
`recommendedEv`, `tags`, `updatedAt`, 그리고 `recommendedMoves[].move` /
`recommendedItems[].item` 슬러그.

언어별로 달라지는 것은 `locale`, `title`, `summary`, `strengths`,
`weaknesses`, `recommendedMoves[].reason`, `recommendedItems[].reason`,
`bodyMarkdown` 뿐이다.

### 슬러그 표기

모든 구조화 필드의 키값은 소문자 kebab-case 영문 슬러그로 고정한다:
`normal`, `fighting`, `parental-bond`, `double-edge`, `life-orb`, `adamant`.

## 3. 대괄호 강조 규칙 (중요)

본문/요약/강점/약점/기술·아이템 reason/제목 등 모든 문자열 필드에서
대괄호 `[...]`는 다음 규칙을 **엄격히** 따른다.

### 3.1 대상: 해당 파일의 키값에 존재하는 슬러그만

대괄호는 **이 파일의 구조화 필드에 실제로 존재하는 슬러그**에 한해서만
붙일 수 있다. 허용 슬러그 집합은 아래 필드에서 추출한다:

- `nameEn`
- `types[]`
- `recommendedAbility`
- `recommendedNature`
- `recommendedTera[]`
- `recommendedMoves[].move`
- `recommendedItems[].item`

허용 집합에 없는 슬러그는 **절대** 대괄호로 감싸지 않는다.

### 3.2 표기: ko/en 모두 영문 슬러그

`locale`과 무관하게 대괄호 안은 **항상 영문 kebab-case 슬러그**로 쓴다.

- 허용: `[fighting]`, `[parental-bond]`, `[double-edge]`, `[kangaskhan-mega]`
- 금지: `[격투]`, `[Fighting]`, `[뻗기]`, `[메가캥카]`, `[Kangaskhan]`

한국어 본문은 자연스러운 한글 문장 안에 영문 슬러그만 대괄호로 삽입한다:

```
[parental-bond]로 모든 공격이 2회 타격으로 변환되는 메가 최상위 물리 에이스.
```

영어 본문도 동일하게 소문자 슬러그만 대괄호에 사용한다:

```
[parental-bond] turns every attack into a double-strike...
```

### 3.3 일반 문맥에서 대괄호를 남용하지 않는다

포켓몬·기술·특성·아이템·타입 용어가 문장 안에 등장한다고 해서 자동으로
대괄호를 두르면 안 된다. 대괄호를 붙이는 조건은 **다음 두 가지를
모두 만족**할 때뿐이다:

1. 해당 슬러그가 **이 파일의 구조화 필드 키값**에 존재
2. 그 용어가 **실체(타입/기술/특성/아이템/주체 포켓몬)**를 지시하는 문맥

대괄호를 넣지 말아야 할 예:

- 다른 포켓몬을 참고로 언급: `... 갸라도스 같은 물 타입 ...`
  → `갸라도스`는 이 파일의 키값이 아니므로 대괄호 X.
- 약점/내성 설명에서의 일반적 타입 언급: `격투 2배 약점` 이더라도
  `fighting`이 `types`/`recommendedTera`/기술에 없다면 대괄호 X.
  (약점으로 언급되는 타입은 키값이 아니므로 일반 텍스트로 쓴다.)
- 아키타입·역할 비유: `피지컬 스위퍼 역할` → `physical-sweeper`가 tags에
  있더라도 `tags`는 허용 집합이 아니므로 대괄호 X.
- 흔한 기술군 통칭: `반동기 운용 주의` → 특정 기술 지시가 아님.

### 3.4 기존 파일 검증

파일을 추가·수정한 뒤 다음 조건을 만족해야 한다:

- 모든 `[...]` 내부 문자열이 **소문자 kebab-case 슬러그**
- 모든 `[...]` 슬러그가 해당 파일의 **허용 집합에 포함**
- 한글 또는 영문 대문자가 대괄호 안에 존재하지 않음
- 중첩 대괄호 (`[X[Y]Z]` 형태) 없음

## 4. bodyMarkdown 섹션 구조

관례적으로 다음 섹션 순서를 유지한다.

**한국어**:
```
## 개요
## 강점 분석
## 약점과 대응
## 추천 기술 구성
## 추천 도구 · 특성 · 테라스탈
## 시너지와 파트너
## 운용 팁
```

**영어**:
```
## Overview
## Strengths
## Weaknesses & Answers
## Recommended Moveset
## Item · Ability · Tera
## Teammates & Synergy
## Play Patterns
```

## 5. updatedAt

`YYYY-MM-DDT00:00:00+09:00` (KST) 형식의 ISO8601 문자열. 내용을 수정했다면
해당 날짜로 갱신한다.
