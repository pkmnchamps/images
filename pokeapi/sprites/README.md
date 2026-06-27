# 포켓몬 챔피언스 — 스프라이트 에셋

PokeAPI(https://github.com/PokeAPI/sprites)에서 수집한 이미지 모음. **별도 정적 호스팅 깃**에 올려 앱이 URL로 로드한다.

## 폴더 구조 (이 폴더를 정적 깃 루트에 그대로 복사)
```
official-artwork/<pokemonId>.png   # 공식 아트워크 — 1337개 (162.2MB)
default/<pokemonId>.png            # 게임 도트 스프라이트 — 1339개 (1.4MB)
items/<itemName>.png               # 도구 스프라이트 — 388개 (0.1MB)
```
- `pokemonId` = PokeAPI pokemon id(폼 포함). 예: 한카리아스 `445`, 메가이상해꽃 `10033`.
- `itemName` = PokeAPI item name. 예: 구애머리띠 `choice-band`, 이상해꽃나이트 `venusaurite`.

## 앱 연결
1. 이 폴더들을 정적 깃에 올린다(예: `https://raw.githubusercontent.com/<user>/<repo>/main/`).
2. 그 raw 베이스 URL을 번들 메타에 설정:
   ```bash
   node tool/build_bundle/set_sprite_base.mjs https://raw.githubusercontent.com/<user>/<repo>/main
   ```
3. 앱은 `meta.spriteBase + "/" + 상대경로`로 로드. 예) `<base>/official-artwork/445.png`.
   - 번들 각 엔트리의 `sprites.officialArtwork` / `sprites.dot`(포켓몬), `sprite`(도구)가 상대경로.
   - `spriteBase`가 비어 있으면 `sprites.source`의 PokeAPI 원본 URL로 폴백 가능.

## 라이선스
Pokémon 이미지 © Nintendo / Game Freak / The Pokémon Company. 비공식 팬/비상업 용도 가정. 배포 시 라이선스·고지 확인.
