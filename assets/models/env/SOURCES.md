# 환경 프롭 출처 (CC0)

이 폴더의 glb는 전부 **Kenney(www.kenney.nl)** 의 CC0 1.0(https://creativecommons.org/publicdomain/zero/1.0/) 킷을
`pnpm art:props <nature-kit-dir> [platformer] [survival] [holiday] [toy-car] [city-kit-suburban] [furniture] [food] [graveyard] [mini-dungeon]`(fit-prop.mjs)로 변환한 것이다:
단일 프리미티브·정점색(COLOR_0)·월드 단위 스케일·(단색 킷은) Lispawn 마스터 팔레트로 재색칠 / (컬러맵 킷은) 텍스처를 정점에 샘플.

| 킷 | 원본 zip | 쓰임 |
|---|---|---|
| Nature Kit 2.1 | https://kenney.nl/assets/nature-kit | 초원(벽·수풀·꽃·풀·돌·나무) + 지형 오브젝트(P57 — 모닥불 `campfire` = 돌 고리 + 장작 두 원본 합침, 키 큰 풀 `tall_grass`) + 사막(사암 벽 `wall_sand`·마른 덤불 `bush_dry_*`·선인장·야자·바위·마른 풀·오벨리스크) — 팔레트 재색칠 |
| Platformer Kit | https://kenney.nl/assets/platformer-kit | 상자(`chest_*`)·에어드랍·무기 크레이트 — 컬러맵 샘플 |
| Survival Kit | https://kenney.nl/assets/survival-kit | 물병·휘발유통(배럴 틴트) — 컬러맵 샘플 |
| Toy Car Kit | https://kenney.nl/assets/toy-car-kit | 놀이터(장난감 자동차 `toy_car_*`/`toy_truck`·콘·블록·원반 `frisbee_*`(동전 재색칠)·장난감 나무) — 컬러맵 샘플 |
| City Kit Suburban | https://kenney.nl/assets/city-kit-suburban | 놀이터(화분 `planter`·동네 나무 `park_tree_*`) — 컬러맵 샘플. 생울타리 `hedge_block`·꽃 관목 `shrub_pink_*`는 Nature Kit 재색칠 |
| Furniture Kit | https://kenney.nl/assets/furniture-kit | 사무실(박스 벽 `box_wall`·화분 `plant_pot_*`·책 `books`·휴지통·사무 의자·노트북·스탠드·책상·책장·TV장) — 텍스처 없이 머티리얼 색(wood/woodDark는 팔레트, 나머진 원색). 도구 정식 모델 `weapon_chair/keyboard`도 여기서(무기 계약) |
| Food Kit | https://kenney.nl/assets/food-kit | 사무실(커피컵 `cup_coffee`·도넛·쿠키) — 컬러맵 샘플. 도구 `weapon_pan`(프라이팬)도 여기서 |
| Graveyard Kit 5.0 | https://kenney.nl/assets/graveyard-kit | 묘비 `gravestone`(P57) — 컬러맵 샘플 + 채널 배율로 팔레트 stone에 맞춤 |
| Mini Dungeon 2.0 | https://kenney.nl/assets/mini-dungeon | 바닥 방어구 `armor_1~3`(P63) — 둥근 방패를 뒤로 70° 눕혀 등급별 크기, 컬러맵 샘플 |
| Holiday Kit | https://kenney.nl/assets/holiday-kit | 설원(눈 덮인 나무 `tree_snow_*`/수풀 `bush_snow_*`·눈더미·바위·선물·사탕지팡이·랜턴·눈사람·썰매·벤치) — 컬러맵 샘플(원색 유지). 얼음 벽 `wall_snow`는 Nature Kit 재색칠 |

바닥 테이프 `tape`(P63)는 킷 원본 없이 fit-prop이 같은 로우폴리 문법으로 절차 생성한다(8각 롤, 팔레트 yellow·tan).

바이옴별 프롭 세트는 `src/render-engine/biome.ts`(표현 전용, 맵 JSON `biome`으로 선택). 지면 텍스처는 `assets/ground/`(`pnpm art:ground`).

CC0라 표기 의무는 없지만, 크레딧 화면·docs/STORE_LISTING.md에 "Kenney (kenney.nl)"을 감사 표기한다.
정식 아트로 교체할 때는 같은 파일명 glb로 덮어쓰면 된다(계약: docs/ART_SPEC.md "환경 프롭").
