# 캐릭터·무기 모델 출처 (CC0)

## 현행 캐릭터: Gobkit Free Animal Pack A·B — 2026-10-02(P54)

**Gobkit**(gobkit.com, Alsomind Tech Co., Ltd. — CC0 1.0, 팩의 LICENSE.txt: "You can copy, modify, distribute and use them, even for commercial
purposes, all without asking permission and with no attribution required")의 공개 zip을 내려받아 `pnpm art:gobkit <animal-dir> <animalB-dir>`(fit-gobkit.mjs)로 변환했다.
로그인 불필요: `https://gobkit.com/freebies/animal/gobkit-animal-pack.zip`, `https://gobkit.com/freebies/animalB/gobkit-animalB-pack.zip`.
같은 회사의 생성 서비스(Forge) 무료 결과물은 비상업 조건이다 — 이 팩(고정된 무료 팩)과 섞지 않는다.

| 파일 | 원본 | 용도 | tris | 비고 |
|---|---|---|---|---|
| gob_rat.glb | Vol.2 `Rat` | mochi(모치) | 532 | 스킨드(원본 뼈 16 + 동공 2 + 팔 2 + 손 2), 클립 idle/run/down |
| gob_red.glb | `Red` | tofu(토푸, 레서판다) | 694 | 〃 |
| gob_corgi.glb | `Corgi` | bori(보리) | 732 | 〃 |
| gob_duck.glb | `Duck` | kkoma(꼬마) | 520 | 〃 (날개 대신 팔) |

변환 규칙(fit-gobkit.mjs):
- **모델 공간으로 다시 굽기**: 정점·노멀을 바인드 포즈의 모델 공간으로 옮기고, 역바인드는 끝에서 rest 뼈의 역행렬로 다시 만든다. 원본은 메시마다 단위·축이
  제각각이다(팩 A는 cm에 z-up 메시, 팩 B는 m, Boar는 역바인드에 ×100) — 아웃라인 폭이 스키닝 전 메시 단위라 그대로 두면 종마다 테 두께가 달라지고(Boar는 화면을 덮는 원반),
  부위를 덧붙일 좌표계도 없다. 스킨드 메시 노드의 변환은 비운다.
- 20종이 **같은 뼈대**(Hips·Spine·Head·다리 4·귀 2·꼬리·입·손 2·눈 2)를 쓴다 — 머리 뼈 높이를 40u로 맞춰 전 종 같은 배율(히트박스 공용). 노드 이동·애니 이동 키에도 굽는다.
- **큰 얼굴 + 긴 팔다리, 두 손으로 총을 든다**(ED 2026-10-02 "총을 손으로 들고 · 캐릭터에 맞는 손과 발 · 발과 손이 길었으면 · 얼굴만 크고"):
  - 팔: 몸 **안**의 어깨(`ARM_PIVOT`)에서 나오는 긴 각기둥(22u) + 큰 매끈한 벙어리장갑 손. 새 뼈 `LeftArm`/`RightArm`·`LeftPaw`/`RightPaw`(몸통 뼈의 자식).
    rest = 바깥·앞으로 비스듬히 늘어뜨린 팔 — 곧게 내리면 손이 땅 가까이 와서 앞다리로 읽혔다. 발가락 혹 달린 손은 뼈다귀로 읽혔다(시각 QA).
    런타임(character-3d `solveArms`)이 손 뼈를 목표(+x 손 = 손잡이, −x 손 = 총 앞쪽 아래)에 두고 팔 뼈를 그쪽으로 돌려 늘인다. 죽음·초상은 rest.
  - 다리: 원래 앞다리·날개(오리)는 지운다(팔이 그 자리). 뒷다리 뼈를 몸 가운데(z −2.5)로 옮겨 조금 벌리고(이동 키도 함께), 긴 다리 + 앞으로 나온 큰 발을 붙인다
    (몸이 `LEG_EXT` 15u 뜬다 — 전 종 같게: 레지스트리 앵커 하나를 같이 쓴다). 오리 발은 넓적한 물갈퀴. 걷기 클립의 뒷다리 흔들림은 ×2.2(두 다리로 서면 원래 ±9°는 발이 거의 안 움직였다).
  - 덧붙인 부위는 원본처럼 각진 로우폴리(면 노멀)이고 UV는 **그 동물의 다리 끝 색 칸**을 가리킨다 — 같은 재질·같은 팔레트라 원래 있던 부위처럼 보인다.
  - 런타임이 읽을 값은 루트 노드 extras `rig`(`arms[].arm/paw/reach`, 손 자리 `hand`).
- **동공 뼈**: 눈알(흰자+동공)이 눈 뼈 하나에 묶여 있어, 동공 정점(팔레트 셀로 구분)을 새 뼈 `LeftPupil`/`RightPupil`로 옮긴다. 노드 extras에
  `range`(굴릴 수 있는 거리)·`radius`·`ax`/`ay`(모델의 옆·위가 눈 뼈 공간에서 어느 쪽인가). 눈 뼈 채널은 클립에서 뺀다 — 눈은 런타임(character-fx EyeRig)이 쥔다.
- 클립: walk→run, dead→down, attack 버림. 눈·앞다리·손 뼈 채널 제거. down 클립의 엉덩이 뼈 수평 이동(뒤로 ≈43u 던짐)은 뺀다(시체가 죽은 자리에 남게).
  `hit`·`pickup`은 없다 — 런타임 절차 연출(젤리·숙임). 안 쓰게 된 버퍼는 정리한다.
- 텍스처(512² 팔레트, 12KB)는 내장 그대로 쓴다(정점색으로 굽지 않는다 — 셀 안 그라데이션이 몸의 명암이다). 머티리얼 `body`, baseColorFactor 1.
- 홍보성 메타데이터(asset.extras의 schema.org 블록)는 걷어 낸다. 저작권 표기는 `asset.copyright`에 남긴다.
- 나머지 16종(마멋·아귀·박쥐·하마·해파리·오리너구리·코뿔소·상어·벌·파랑새·멧돼지·복어·염소·부엉이·물범·고래)은 `--all`로 같은 변환이 된다 —
  종을 바꾸거나 늘리려면 매니페스트의 `adopt`와 레지스트리 한 줄. 생김새는 `docs/art-refs/p54-look/1-roster-20.jpg`.

## 총기 9종 + 이전 세대 캐릭터: Kenney Blaster Kit · Cube Pets — 2026-09-12

> 캐릭터(pet_*.glb)는 P54에서 Gobkit으로 바뀌었다 — 파일은 dev 비교(`?look=kenney`)용으로 남아 있다.

둘 다 **Kenney**(www.kenney.nl, CC0 1.0 — https://creativecommons.org/publicdomain/zero/1.0/)의 공개 zip
(`kenney.nl/assets/cube-pets`, `kenney.nl/assets/blaster-kit`, 로그인 불필요)에서 내려받아 `pnpm art:kenney <cubepets-dir> <blaster-dir>`
(fit-kenney.mjs)로 변환했다. 환경 프롭(Nature Kit, `env/`)과 같은 작가라 톤이 맞는다.

| 파일 | 원본 | 용도 | tris | 비고 |
|---|---|---|---|---|
| pet_cat.glb | animal-cat | tofu(두부 고양이) | 684 | 노드 애니 idle/walk/run/eat/dance/gesture-* + 합성 hit/down |
| pet_dog.glb | animal-dog | bori(강아지) | 490 | 〃 |
| pet_chick.glb | animal-chick | kkoma(병아리) | 490 | 〃 |
| pet_pig.glb | animal-pig | mochi(찐빵·분홍) | 424 | 〃 |
| weapon_pistol.glb | blaster-k | 권총 | 392 | 길이 28 |
| weapon_smg.glb | blaster-i | SMG | 416 | 30 |
| weapon_shotgun.glb | blaster-g | 샷건 | 618 | 38 |
| weapon_rifle.glb | blaster-d | 소총 | 486 | 40 |
| weapon_revolver.glb | blaster-n | 리볼버 | 410 | 30 |
| weapon_water_gun.glb | blaster-b | 물총 | 368 | 30 |
| weapon_dart_gun.glb | blaster-m | 마취총 | 440 | 32 |
| weapon_firework.glb | blaster-o | 폭죽포(4연장) | 664 | 34 |
| weapon_rail_gun.glb | blaster-f | 레일건(스코프) | 768 | 40 |

변환 규칙(fit-kenney.mjs):
- Kenney 컬러맵(8×4 팔레트 셀, 셀 안 명암 그라데이션)을 정점 UV에서 샘플해 **정점색(COLOR_0, linear)**으로 굽는다 — 텍스처/UV 제거, 파일 1개.
- 무기: 면적 최대 셀 = `body`(baseColorFactor=셀 대표색, 정점색=비율) / 나머지 = `detail`(고정색). **원색 그대로** 보이되 `body`는 무기 스킨 틴트 대상.
  캐릭터: 틴트를 쓰지 않으므로(레지스트리 `tint: []`, ED 결정 — 플레이어 8색은 아웃라인·HP바·이름표에만) 분리하지 않는다 —
  메시당 프리미티브 1개(`body` 흰 바탕 + 정점색 원색). 노드가 7~9개라 프리미티브 수가 곧 드로콜(+아웃라인)이다: 캐릭터당 24 → 14.
- 스케일·발 y=0(캐릭터, 몸통 1.58u→46) / 총열 +Z·원점=그립(무기, Kenney 규약은 총열 -Z라 전부 반전)을 정점·노드 이동·애니 키에 굽는다.
- 노드 계층·노드 애니 보존(스킨 없음). 계약 클립 `hit`(뒤로 밀림+스쿼시 0.3s)·`down`(옆으로 넘어짐 0.6s)은 루트 노드 TRS로 합성.
- CC0라 표기 의무는 없지만 크레딧 화면·docs/STORE_LISTING.md에 "Kenney (kenney.nl)"을 감사 표기한다.
- 같은 팩의 나머지(동물 20종, 블래스터 9종, 총알/탄창/스코프/수류탄/표적)는 같은 경로로 추가 반입 가능(매니페스트에 한 줄).

## 도구 정식 모델(P38, 2026-09-30) — Kenney Furniture Kit · Food Kit(CC0)

`pnpm art:props … [furniture] [food]`(fit-prop.mjs의 `weapon:` 항목)이 무기 계약(원점 = 손잡이, 때리는 쪽 +Z, 머티리얼 `body`, 정점색)으로 변환해 이 폴더에 낸다.
gen-models 플레이스홀더를 같은 파일명으로 덮어쓰며, `pnpm art:models`는 자기 것이 아닌 glb를 건너뛴다.

| 파일 | 원본 | 용도 | tris | 비고 |
|---|---|---|---|---|
| weapon_chair.glb | Furniture `chair` | 의자(도구, 3방에 박살) | 170 | rotX −90 — 등받이 위를 잡고 다리를 앞으로, 길이 34 |
| weapon_keyboard.glb | Furniture `computerKeyboard` | 키보드(도구, 연타) | 32 | rotY −90 — 짧은 변을 잡고 긴 쪽 앞으로, 길이 30 |
| weapon_pan.glb | Food `frying-pan` | 프라이팬(도구) | 200 | 컬러맵 샘플, 손잡이(−z 좁은 끝)가 이미 뒤, 길이 30 |

빗자루(`weapon_broom.glb`)는 아직 절차 생성(gen-models).

## 이전 세대(파일 유지 — 레지스트리 glb 파일명만 바꾸면 되돌아간다)

- `q_*.glb` 4종: **Quaternius "3D Colorful Monsters"**(CC0) 리깅 모델(2026-09-05, GDevelop 에셋 스토어 공개 CDN
  `asset-resources.gdevelop.io/public-resources/3D Colorful Monsters/…`). 스킨드라 `art:fit` 불가 → 레지스트리 `scale/tint`(`*_Main`) +
  `pickClips` 별칭(Idle/Walk/HitRecieve/Death). q_pinkblob(mochi)·q_cat(tofu)·q_dog(bori)·q_chicken(kkoma).
- `mochi.glb` 등 절차 플레이스홀더(`pnpm art:models`, gen-models.mjs) — 활·석궁·검·프라이팬·망치·모자·의상은 지금도 이것.
