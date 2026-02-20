# TIMEFOLIO ETF 추적기 v2

17개 TIMEFOLIO 액티브 ETF의 구성종목 데이터를 매일 자동 수집하고 웹으로 보여주는 정적 사이트입니다.

## 구조

```
deploy_v2/
├── index.html                          ← 프론트엔드 (정적 HTML)
├── data/
│   ├── latest/                         ← 프론트엔드가 fetch하는 JSON
│   │   ├── holdings.json
│   │   ├── shares.json
│   │   ├── summaries_weight.json
│   │   ├── summaries_shares.json
│   │   └── last_updated.json
│   └── history/                        ← 일별 스냅샷 누적
│       ├── holdings/YYYY-MM-DD.json
│       └── shares/YYYY-MM-DD.json
├── scripts/
│   ├── constants.js                    ← ETF 목록, 설정 공유 모듈
│   ├── update.js                       ← 크롤링 스크립트
│   └── build_latest.js                 ← latest JSON 빌드
├── .github/workflows/
│   └── update-and-deploy.yml           ← 매일 23:00 UTC 자동 실행
├── package.json
└── README.md
```

## 배포 방법 (GitHub Pages)

1. 이 폴더를 GitHub 저장소에 push
2. Settings → Pages → Source: **GitHub Actions** 선택
3. 워크플로우가 매일 23:00 UTC (08:00 KST)에 자동 실행됨

## 수동 실행

```bash
# 오늘 날짜로 크롤링
node scripts/update.js

# 특정 날짜로 크롤링
node scripts/update.js 2026-02-20

# latest JSON 빌드
node scripts/build_latest.js

# 크롤링 + 빌드 한번에
npm run update-and-build
```

## 워크플로우 수동 트리거

GitHub Actions 탭 → "Daily ETF Update & Deploy" → Run workflow → 날짜 입력(선택)

## 데이터 출처

[timeetf.co.kr](https://timeetf.co.kr) 구성종목 페이지에서 크롤링
