# UI 폰트 (ART_DIRECTION §3) — SIL Open Font License 1.1

| 파일 | 원본 | 용도 | 서브셋 |
|---|---|---|---|
| jua.woff2 | Jua Regular — github.com/google/fonts `ofl/jua` (Copyright 2018 The Jua Project Authors) | 한글 UI(둥근 고딕) | KS X 1001 완성형 한글 2350자 + ASCII + 기호, 353KB (원본 ttf 2.1MB) |
| baloo2.woff2 | Baloo 2 가변(wght 400~800) — github.com/google/fonts `ofl/baloo2` (Copyright 2019 The Baloo 2 Project Authors) | 숫자·영문 | Latin(U+0020-00FF) + 구두점·₩·∞, 31KB (원본 ttf 683KB) |

라이선스 전문: `OFL-Jua.txt`, `OFL-Baloo2.txt`. OFL은 앱에 번들·재배포를 허용한다(폰트 단독 판매 금지, 라이선스 동봉).

재생성: `pip install fonttools brotli` 후
`pyftsubset Jua-Regular.ttf --text-file=<KS X 1001 2350자+ASCII+기호> --flavor=woff2 --layout-features='*'`,
`pyftsubset 'Baloo2[wght].ttf' --unicodes='U+0020-007E,U+00A0-00FF,U+2013,U+2014,U+2018,U+2019,U+201C,U+201D,U+2026,U+20A9,U+00D7,U+221E' --flavor=woff2 --layout-features='*'`.
서브셋에 없는 글자(완성형 밖 한글 등)는 시스템 폰트로 대체된다.
