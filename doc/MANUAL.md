# 📖 제작 매뉴얼 — 함명인 간사 개인 사역 홈페이지

> **프로젝트:** 함명인 간사 개인 사역 홈페이지  
> **기술 스택:** Hugo (Extended), Hugo Blox SaaS Landing Page 템플릿, Tailwind CSS v4, Node.js  
> **저장소:** [annieham123498-tech/mywebsite](https://github.com/annieham123498-tech/mywebsite)  
> **최종 업데이트:** 2026-07-06

---

## 목차

1. [프로젝트 개요](#1-프로젝트-개요)
2. [환경 요구사항](#2-환경-요구사항)
3. [로컬 개발 환경 설정](#3-로컬-개발-환경-설정)
4. [디렉토리 구조](#4-디렉토리-구조)
5. [핵심 설정 파일 가이드](#5-핵심-설정-파일-가이드)
6. [콘텐츠 편집 방법](#6-콘텐츠-편집-방법)
7. [블로그 글 작성 방법](#7-블로그-글-작성-방법)
8. [GitHub 배포 방법](#8-github-배포-방법)
9. [문제 해결 (Troubleshooting)](#9-문제-해결-troubleshooting)

---

## 1. 프로젝트 개요

이 홈페이지는 미국 뉴저지 아이하나 교회 사역 간사인 **함명인 간사**의 개인 사역 포트폴리오 및 소통 창구입니다.

| 항목 | 내용 |
|------|------|
| 생성기 | Hugo v0.163.3 (Extended) |
| 테마 | Hugo Blox SaaS Landing Page |
| CSS 엔진 | Tailwind CSS v4 |
| 주요 언어 | 한국어 (ko-kr) |
| 폰트 | Noto Serif KR (Google Fonts) |
| 색상 테마 | 따뜻한 파스텔 톤 (세이지 그린, 베이지, 브라운) |

---

## 2. 환경 요구사항

| 도구 | 버전 | 설치 방법 |
|------|------|-----------|
| Hugo Extended | v0.163.3 이상 | `winget install Hugo.Hugo.Extended` |
| Node.js | v20 이상 | `winget install OpenJS.NodeJS.LTS` 또는 포터블 버전 사용 |
| npm | v10 이상 | Node.js 설치 시 포함 |
| Git | v2.x | `winget install Git.Git` |
| GitHub CLI | v2.x | `winget install GitHub.cli` |
| Go | v1.19 이상 | Hugo 모듈 사용 시 필요 (`winget install GoLang.Go`) |

> **참고:** 이 프로젝트는 `node-portable/` 폴더에 포터블 Node.js v20.11.0이 포함되어 있습니다. (`.gitignore`에 의해 git에는 제외됨)

---

## 3. 로컬 개발 환경 설정

### 3-1. 저장소 클론

```bash
git clone https://github.com/annieham123498-tech/mywebsite.git
cd mywebsite
```

### 3-2. 의존성 설치

```powershell
npm install
```

> **오류 발생 시:** npm이 인식되지 않으면 Node.js PATH를 먼저 설정합니다:
> ```powershell
> $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine") + ";" + $env:Path
> ```

### 3-3. Hugo 모듈 다운로드

```powershell
hugo mod download
```

### 3-4. 로컬 개발 서버 실행

```powershell
hugo server --disableFastRender
```

브라우저에서 `http://localhost:1313` 접속하여 미리보기.

### 3-5. 프로덕션 빌드

```powershell
hugo --minify
```

---

## 4. 디렉토리 구조

```
myung in ham/                  # 프로젝트 루트
├── assets/
│   ├── css/
│   │   └── custom.css         # 커스텀 폰트·스타일 오버라이드
│   └── media/                 # 이미지·미디어 파일
├── config/
│   └── _default/
│       ├── hugo.yaml          # Hugo 기본 설정
│       ├── languages.yaml     # 언어 설정 (ko)
│       ├── menus.yaml         # 네비게이션 메뉴
│       ├── module.yaml        # Hugo 모듈 설정
│       └── params.yaml        # 사이트 파라미터·테마·SEO
├── content/
│   ├── _index.md              # 홈페이지 메인 (섹션 블록 정의)
│   ├── blog/                  # 블로그 글 폴더
│   │   ├── _index.md
│   │   ├── letter-from-earth-end/   # "땅끝에서 전하는 편지" 카테고리
│   │   └── grace-care-meditation/   # "은혜의 돌봄 묵상" 카테고리
│   └── authors/               # 저자 정보
├── data/
│   └── authors/
│       └── me.yaml            # 함명인 간사 프로필 데이터
├── doc/
│   ├── MANUAL.md              # 📖 이 파일 (제작 매뉴얼)
│   └── ISSUES.md              # 🐛 문제 보고서
├── layouts/
│   └── partials/
│       └── blox/
│           └── contact.html   # 커스텀 연락처 폼 블록
├── plan.md                    # 콘텐츠 기획서
├── package.json               # npm 스크립트·의존성
├── go.mod                     # Hugo 모듈 정의
└── README.md                  # 프로젝트 소개 (GitHub용)
```

---

## 5. 핵심 설정 파일 가이드

### 5-1. `config/_default/params.yaml` — 사이트 정보 설정

사이트의 이름, 설명, 색상, 메뉴, 푸터 등 대부분의 설정이 여기에 있습니다.

```yaml
hugoblox:
  identity:
    name: "함명인 간사"              # 사이트 이름 (네비바·푸터에 표시)
    tagline: "..."                    # 한 줄 소개
    description: "..."               # SEO 메타 설명
  theme:
    mode: light                       # light | dark | system
    colors:
      primary: "#5a7356"              # 세이지 그린 (메인 색상)
      secondary: "#8b7355"            # 따뜻한 브라운
      neutral: "stone"                # 베이지 계열 회색
  typography:
    pack: "geometric"
  seo:
    title: "함명인 간사 | ..."        # 브라우저 탭 제목
```

### 5-2. `content/_index.md` — 홈페이지 섹션 구성

홈페이지는 YAML 프론트매터의 `sections` 배열로 블록을 쌓아 구성합니다:

| 블록 ID | 블록 타입 | 내용 |
|---------|-----------|------|
| `top` | `hero` | 헤드라인·CTA 버튼 |
| `about` | `cta-image-paragraph` | 사역 스토리·성경구절 |
| `strengths` | `features` | 3가지 사역 은사 |
| `ministry` | `features` | 전도·돌봄 사역 카드 |
| `timeline` | `steps` | 사역 이력 타임라인 |
| `blog` | `collection` | 최근 블로그 글 목록 |
| `contact` | `contact` | 연락처 문의 폼 |

### 5-3. `assets/css/custom.css` — 폰트·스타일 커스터마이징

```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Serif+KR:wght@300;400;500;700&display=swap');

body, h1, h2, h3, p, ... {
  font-family: 'Noto Serif KR', serif !important;
}
```

---

## 6. 콘텐츠 편집 방법

### 헤드라인 변경

`content/_index.md` 파일에서 `block: hero` 섹션의 `title`과 `text`를 수정합니다:

```yaml
- block: hero
  content:
    title: "새로운 헤드라인 텍스트"
    text: "새로운 서브카피 텍스트"
```

### 사역 소개 카드 수정

`block: features` (id: ministry)의 `items` 배열을 수정합니다:

```yaml
- name: "새 사역 이름"
  icon: hero/아이콘이름
  description: "사역 설명"
```

> **아이콘 참고:** [Heroicons](https://heroicons.com) 사이트에서 아이콘 이름 확인 후 `hero/이름` 형식으로 입력

### 프로필 사진 변경

`assets/media/` 폴더에 `about-profile.jpg` 파일을 교체합니다.

---

## 7. 블로그 글 작성 방법

`content/blog/` 폴더에 새 폴더를 만들고 `index.md` 파일을 작성합니다.

```bash
content/blog/새글폴더이름/index.md
```

### 예시 프론트매터

```yaml
---
title: "글 제목"
summary: "한 줄 요약"
date: 2026-07-06
authors:
  - me
categories:
  - "땅끝에서 전하는 편지"   # 또는 "은혜의 돌봄 묵상"
tags:
  - "전도 사역"
---

본문 내용을 Markdown으로 작성합니다.
```

---

## 8. GitHub 배포 방법

### 변경사항 push

```powershell
git add .
git commit -m "커밋 메시지 (한국어 가능)"
git push origin main
```

### 최초 인증 (GitHub CLI)

```powershell
gh auth login --web --hostname github.com
# 브라우저에서 코드 입력하여 인증
```

### workflow 권한 추가 (GitHub Actions 파일 변경 시)

```powershell
gh auth refresh -h github.com -s workflow
```

---

## 9. 문제 해결 (Troubleshooting)

자세한 문제 보고 및 해결 이력은 [ISSUES.md](./ISSUES.md)를 참조하세요.

| 증상 | 원인 | 해결 방법 |
|------|------|-----------|
| `hugo` 명령어 인식 안됨 | PATH 미설정 | `$env:Path` 재로드 또는 터미널 재시작 |
| `npm install` 실패 | node 인식 안됨 | npm 실행 시 node-portable PATH 포함 |
| push 403 오류 | 저장소 권한 없음 | 올바른 계정으로 `gh auth login` |
| push workflow 오류 | workflow scope 없음 | `gh auth refresh -s workflow` |
| Hugo 빌드 오류 | 모듈 미다운로드 | `hugo mod download` 실행 |
