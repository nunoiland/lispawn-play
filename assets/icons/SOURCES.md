# UI 아이콘 — 출처·라이선스

전부 단색 글리프(투명 배경). 화면에선 CSS 마스크로 칠한다(`ui-dom/icons.ts` `icon()` — 색은 `tokens.ts`).

## Kenney (www.kenney.nl) — CC0 1.0 (https://creativecommons.org/publicdomain/zero/1.0/)

공개 zip(로그인 불필요)을 풀어 `pnpm art:icons <game-icons> <game-icons-expansion> <board-game-icons> <crosshair-pack>`로 반입했다
(fit-icons.mjs의 MANIFEST가 역할 이름 ← 원본 파일 대응의 정본). 픽셀은 원본 그대로이고 PNG만 다시 인코딩했다(원본은 압축이 안 돼 있어 31장 366KB → 30KB). 환경 프롭·캐릭터·총기와 같은 작가라 톤이 맞는다.

| 팩 | 주소 | 쓰는 아이콘 |
|---|---|---|
| Game Icons | kenney.nl/assets/game-icons | settings back exit pause shop training play prev quest check trophy lock replay ad report sound sound_off solo duo squad wide narrow (100×100) |
| Game Icons Expansion | kenney.nl/assets/game-icons-expansion | coin fists(← fightFist, P62) (100×100) |
| Board Game Icons 1.1 | kenney.nl/assets/board-game-icons | move pickup skill swap skull locker again armor(← shield) juice(← flask_full) (128×128) |
| Crosshair Pack | kenney.nl/assets/crosshair-pack | aim ← crosshair-008, Light 2배(128×128) |

크로스헤어 팩의 2배 폴더명은 `Light (2×)`(곱셈 기호)라 macOS `unzip`이 풀다 실패한다 — Finder로 풀거나 Python `zipfile`로 푼다.

## 직접 그린 것

| 파일 | 내용 |
|---|---|
| emote.svg | 감정(이모트) 버튼 — 웃는 얼굴. Kenney Emotes Pack(CC0)은 32px라 폰(3배 밀도)에서 흐려 같은 굵기로 새로 그렸다. |
| camera.svg | 시점 전환 버튼(P45) — 비디오 카메라(캠코더: 몸통 + 옆 렌즈) 실루엣. 팩의 `video`는 44 버튼에서 카메라로 안 읽혔고, 처음 그린 사진기는 "촬영" 느낌이라 시점 전환으로 안 읽혔다(ED 2026-10-02). |
| heal.svg | 회복 버튼(P47) — 둥근 십자. 주스 마시기·테이프 감기를 한 버튼이 맡는다. |
| tape.svg | 테이프 재고(P62) — 테이프 롤(가운데 구멍 + 풀린 끝). 팩에 맞는 글리프가 없었다. |

## 무기·투척물 실루엣 — `weapons/` (P62, SAR식 인벤토리 HUD)

| 파일 | 만든 방법 |
|---|---|
| `<무기 id>.png`, `throw_gas_can.png`, `throw_water_bottle.png` | `pnpm art:weapon-icons`(gen-weapon-icons.mjs)가 게임 glb(Kenney Blaster Kit 총기·도구 정식 모델·지면 소품 — 전부 CC0)를 옆(석궁·프라이팬은 위)에서 본 단색 실루엣으로 굽는다. 256×128, 흰색 + 알파 |
| `bow.svg` `keyboard.svg` `chair.svg` `throw_plate.svg` `throw_banana.svg` | 직접 그림 — 활·키보드·의자는 플레이스홀더 모델이 상자라 어느 쪽에서 봐도 안 읽혔고, 접시·바나나는 지면 모델이 프리미티브다 |
