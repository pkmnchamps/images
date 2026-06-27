# images

포켓몬 관련 정적 이미지·데이터 에셋 저장소. 앱이 raw URL(`https://raw.githubusercontent.com/<user>/images/main/...`)로 직접 로드한다.

## 경로별 가이드

### `sprites/` — 포켓몬 프로필 스프라이트 (1026개)
- `sprites/<도감번호>_profile.png` — 4자리 0패딩 전국도감 번호. 예) `0001_profile.png`(이상해씨), `0445_profile.png`(한카리아스).
- `sprites/forms/<이름>-<폼>.png` — 폼 변경/리전폼 스프라이트 (214개).
  - 폼 접미사: `mega`(메가, 75) · `champs`(챔피언스) · `galar`(가라르) · `alola`(알로라) · `hisui`(히스이) · `therian`(영물폼) · `x`/`y`(메가 X/Y) · `primal`(원시) · `rider`(기수폼) 등.
  - 예) `charizard-mega-x.png`, `arcanine-hisui.png`, `calyrex-ice-rider.png`.

### `items/` — 도구 스프라이트 (955개)
- `items/<itemName>.png` — PokeAPI item name 기준. 예) `choice-band.png`(구애머리띠), `venusaurite.png`(이상해꽃나이트), `leftovers.png`(먹다남은음식).

### `icons/` — UI 아이콘
- `icons/types/<타입>.png` — 18개 타입 아이콘. 예) `fire.png`, `water.png`, `dragon.png`.
- `icons/move_types/<분류>.png` — 기술 분류 3종: `move-physical.png`(물리) · `move-special.png`(특수) · `move-status.png`(변화).
- `icons/megaicon.webp` — 메가진화 표시 아이콘.

### `forum/` — 포켓몬 배틀 운용 가이드 (JSON, 385개)
- `forum/<도감번호>[-<폼>].<locale>.json` — 포켓몬별 운용 가이드 데이터.
  - locale: `ko`(129) · `ja`(129) · `en`(127) 3개 언어.
  - 폼 변형 예) `115-mega.ko.json`(메가캥카).
- 주요 필드: `pokemonId`, `nameKo`/`nameEn`, `formKey`, `types`, `roles`, `recommendedAbility`, `recommendedNature`, `recommendedTera`, `recommendedEv`, `title`, `summary`, `strengths` 등.

### `pokeapi/` — PokeAPI 정제 데이터
PokeAPI(pokeapi.co/api/v2) 전국도감 데이터를 lean하게 정제한 JSON 모음.
- `index.json` — 생성 시각·집계(counts)·범위(scope) 메타.
- `pokemon.json` (≈10MB) — 포켓몬 1351종. version_group_details·전세대 스프라이트 트리 제거.
- `species.json` — 종 정보 1025종.
- `moves.json` — 기술 833개.
- `abilities.json` — 특성 312개.
- `items.json` — 도구 450개.
- `types.json` — 타입 18개.
- `evolution-chains.json` — 진화 트리 541개.
- `cache/` — PokeAPI 원본 전체 응답 캐시 (`ability/`, `berry/`, `evolution-chain/`, `item/`, `move/`, `pokemon/`, `pokemon-species/`, `type/`).
- `sprites/` — 정적 호스팅용 스프라이트 (자세한 내용은 `pokeapi/sprites/README.md`).
  - `official-artwork/<pokemonId>.png` — 공식 아트워크 (1337개, 상세 화면용).
  - `default/<pokemonId>.png` — 게임 도트 스프라이트 (1339개).
  - `items/<itemName>.png` — 도구 스프라이트 (388개).
  - `manifest.json` — 스프라이트 메타·라이선스 정보.

### 루트 파일
- `og-image.png` — OG(소셜 공유) 미리보기 이미지.

## 라이선스
Pokémon 이미지·데이터 © Nintendo / Game Freak / The Pokémon Company. 비공식 팬·비상업 용도 가정. 배포 시 라이선스·고지 확인.
