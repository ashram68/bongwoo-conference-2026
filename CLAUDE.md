# CLAUDE.md — 2026 제3회 봉우학술대회 랜딩페이지

Claude Code가 이 프로젝트에서 작업할 때 참고할 컨텍스트 문서.

## 프로젝트 개요

- **내용**: 사단법인 한국연정원 주최 "2026 제3회 봉우학술대회" 소개 랜딩 페이지 (한국어)
- **형태**: 순수 정적 사이트 — HTML + CSS + 미디어 파일만 사용. 빌드 도구/프레임워크/번들러 **없음**
- **배포**: Vercel (GitHub 연동 자동 배포)
- **언어**: 한국어 (`<html lang="ko">`), Noto Serif KR / Noto Sans KR 웹폰트

## 디렉터리 구조

```
./
├── index.html              # 전체 랜딩페이지 (단일 파일)
├── assets/
│   ├── css/style.css       # 모든 스타일
│   ├── images/             # 배경, 섹션 일러스트, 히어로 사진 등
│   └── videos/             # break1/break2/closing/special.mp4
├── .gitignore
├── .vercelignore
└── .vercel/                # Vercel 링크 정보 (gitignore됨)
```

### 저장소에 올리지 않는 것 (`.gitignore` + `.vercelignore`)

HTML이 실제로 참조하는 `assets/` 외의 아래 항목은 **git/배포 모두에서 제외**:

- `/bw_01.jpg`, `/logo.png` (루트 중복 사본)
- `/docs/` (PDF 등 참고 자료)
- `/images/` (KakaoTalk 사진 원본 — 루트 폴더)
- `/sample/` (참고용 샘플 HTML/이미지)
- `.claude/`, `.vercel/`, `node_modules/` 등

## `.vercelignore` 작성 규칙 (중요)

루트 폴더만 제외하고 싶을 때는 반드시 **루트 앵커(`/`)를 앞에 붙일 것**:

```
/images/          ← 루트의 images/ 폴더만
images/           ← 모든 경로의 images/ 매칭 (assets/images/까지 제외됨)
```

이 사이트는 `assets/images/` 폴더를 쓰기 때문에 앵커 없이 `images/`로 적으면 실제 배포에서 **이미지가 전부 빠지는 사고**가 납니다. 과거 두 번 발생했던 이슈. 수정 후 반드시 **커밋+푸시**까지 해야 GitHub 자동 배포에 반영됨.

## 배포 워크플로우

1. 로컬에서 수정 → `git add` → `git commit` → `git push`
2. Vercel이 GitHub push를 감지해 자동 재배포
3. 고정 프로덕션 URL: `https://bongwoo-conference-2026.vercel.app`
4. CLI에서 수동 배포가 필요하면: `vercel --prod`

변경 사항 반영 안 보이면 브라우저 **강력 새로고침(Ctrl+Shift+R)**. 파비콘은 캐시가 특히 강하므로 시크릿 창으로 확인.

## 작업 시 주의사항

- **파일 경로는 모두 상대 경로**로 유지 (절대 경로 금지): `assets/images/...`
- `index.html` 단일 파일로 모든 섹션을 담고 있음 — 구조 크게 바꾸지 말 것
- 미디어 파일 추가 시 실제 파일이 `assets/images/` 또는 `assets/videos/`에 존재하는지 확인
- 큰 동영상을 추가할 때는 용량 확인 (현재 전체 배포 ~42 MB)
- Korean 한자/특수문자가 많으므로 항상 **UTF-8**로 저장
- 주석은 불필요하게 달지 말 것 (프로젝트 규약: 코드 주석 최소화)

## 파비콘

`<link rel="icon" href="assets/images/logo.png">` 로 설정. `logo.png`는 60×60 px PNG.

## 연관 외부 서비스

| 서비스 | 용도 | 계정 |
|---|---|---|
| GitHub | 소스 저장 | `ashram68/bongwoo-conference-2026` |
| Vercel | 배포 호스팅 | `ashram68-5936` (team: `ashram68-gmailcoms-projects`) |
