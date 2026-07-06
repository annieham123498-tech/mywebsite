# 🐛 문제 보고서 (Issue Log) — 함명인 간사 개인 사역 홈페이지

> **프로젝트:** 함명인 간사 개인 사역 홈페이지  
> **저장소:** [annieham123498-tech/mywebsite](https://github.com/annieham123498-tech/mywebsite)  
> **최종 업데이트:** 2026-07-06

---

## 목차

- [미해결 이슈 (Open)](#미해결-이슈-open)
- [해결된 이슈 (Resolved)](#해결된-이슈-resolved)
- [알려진 제한사항 (Known Limitations)](#알려진-제한사항-known-limitations)

---

## 미해결 이슈 (Open)

| # | 날짜 | 우선순위 | 제목 | 상태 |
|---|------|----------|------|------|
| - | - | - | 현재 미해결 이슈 없음 | - |

---

## 해결된 이슈 (Resolved)

---

### ✅ ISSUE-001 — Node.js 설치 시 UAC(관리자 권한) 팝업으로 인한 설치 중단

| 항목 | 내용 |
|------|------|
| **발생일** | 2026-07-02 |
| **해결일** | 2026-07-02 |
| **심각도** | 중간 (Medium) |
| **범주** | 환경 설정 |

**증상:**  
`winget install OpenJS.NodeJS.LTS` 실행 시 MSI 설치 관리자가 UAC 권한 요청 팝업을 표시하고 무한 대기 상태에 빠짐.

**원인:**  
Node.js LTS 버전은 MSI 인스톨러를 사용하며, 이는 시스템 레벨 설치를 위해 관리자 권한이 필요함.

**해결 방법:**  
포터블(Portable) Node.js v20.11.0을 직접 다운로드·압축 해제하여 사용:
```powershell
Invoke-WebRequest -Uri "https://nodejs.org/dist/v20.11.0/node-v20.11.0-win-x64.zip" -OutFile "node.zip"
Expand-Archive -Path "node.zip" -DestinationPath "node-portable"
Remove-Item "node.zip"
```

실행 시 PATH에 포터블 node 경로 추가:
```powershell
$env:Path = "c:\Users\USER\Desktop\myung in ham\node-portable\node-v20.11.0-win-x64;" + $env:Path
npm install
```

**예방 조치:**  
`node-portable/` 폴더를 `.gitignore`에 추가하여 저장소에 포함되지 않도록 처리.

---

### ✅ ISSUE-002 — `npm install` 실패: `@parcel/watcher` node 명령어 인식 불가

| 항목 | 내용 |
|------|------|
| **발생일** | 2026-07-02 |
| **해결일** | 2026-07-02 |
| **심각도** | 높음 (High) |
| **범주** | 패키지 설치 |

**증상:**  
```
npm ERR! command failed
npm ERR! 'node' is not recognized as an internal or external command
```
`@parcel/watcher` 패키지의 빌드 스크립트가 `node` 명령어를 찾지 못함.

**원인:**  
포터블 Node.js의 경로가 시스템 PATH에 등록되지 않아, npm의 하위 프로세스에서 `node` 실행 불가.

**해결 방법:**  
npm 실행 전 현재 PowerShell 세션의 PATH에 포터블 node 경로를 포함:
```powershell
$env:Path = "c:\...\node-portable\node-v20.11.0-win-x64;" + $env:Path
npm install
```

---

### ✅ ISSUE-003 — `git push` 403 오류: 저장소 권한 없음

| 항목 | 내용 |
|------|------|
| **발생일** | 2026-07-06 |
| **해결일** | 2026-07-06 |
| **심각도** | 높음 (High) |
| **범주** | GitHub 배포 |

**증상:**  
```
remote: Permission to ccumgol/jinguseo.git denied to annieham123498-tech.
fatal: unable to access: The requested URL returned error: 403
```

**원인:**  
최초 `git remote`가 `ccumgol/jinguseo` 저장소로 설정되었으나, 인증된 계정은 `annieham123498-tech`로 해당 저장소에 쓰기 권한 없음.

**해결 방법:**  
remote URL을 `annieham123498-tech` 계정 소유 저장소로 변경:
```powershell
git remote set-url origin https://github.com/annieham123498-tech/mywebsite.git
```

---

### ✅ ISSUE-004 — `git push` workflow 오류: `.github/workflows` 파일 push 거부

| 항목 | 내용 |
|------|------|
| **발생일** | 2026-07-06 |
| **해결일** | 2026-07-06 |
| **심각도** | 중간 (Medium) |
| **범주** | GitHub 배포 |

**증상:**  
```
remote rejected: refusing to allow an OAuth App to create or update workflow
`.github/workflows/build.yml` without `workflow` scope
```

**원인:**  
GitHub CLI 인증 토큰에 `workflow` 스코프가 없어, GitHub Actions 워크플로우 파일 변경이 거부됨.

**해결 방법:**  
GitHub CLI로 `workflow` 스코프를 추가 인증:
```powershell
gh auth refresh -h github.com -s workflow
# 브라우저에서 장치 코드 입력 후 승인
```

---

### ✅ ISSUE-005 — `gh auth login --web` 타임아웃: 브라우저 자동 열기 실패

| 항목 | 내용 |
|------|------|
| **발생일** | 2026-07-06 |
| **해결일** | 2026-07-06 |
| **심각도** | 낮음 (Low) |
| **범주** | GitHub 인증 |

**증상:**  
```
failed to authenticate via web browser: context deadline exceeded
```
`gh auth login --web` 실행 시 브라우저 자동 실행 실패 또는 사용자가 코드 입력 전 만료.

**원인:**  
PowerShell 자동화 환경에서 브라우저 자동 실행이 불가하거나, 장치 코드의 유효 시간(약 15분) 내에 입력이 이루어지지 않음.

**해결 방법:**  
터미널 출력에 표시된 장치 코드(`XXXX-XXXX`)를 수동으로 복사하여 `https://github.com/login/device`에 접속 후 입력.  
명령을 재실행하여 새 코드 발급:
```powershell
gh auth login --web --hostname github.com
```

---

## 알려진 제한사항 (Known Limitations)

| # | 항목 | 설명 | 대안 |
|---|------|------|------|
| L-001 | 포터블 Node.js PATH | 새 터미널 세션마다 PATH를 수동으로 재설정해야 함 | Node.js를 정식 설치(MSI)하여 시스템 PATH에 영구 등록 |
| L-002 | contact 폼 백엔드 없음 | 정적 사이트이므로 폼 데이터가 자동 처리되지 않음 | Netlify Forms 또는 Formspree 연동 필요 |
| L-003 | 프로필 사진 미설정 | about 섹션에 임시 이미지가 표시됨 | `assets/media/about-profile.jpg` 파일 교체 필요 |
| L-004 | Hugo 모듈 캐시 | Go 설치 없이는 `hugo mod download` 불가 | Go 설치 후 모듈 캐시 생성 (`winget install GoLang.Go`) |

---

## 이슈 작성 양식

새 이슈 발생 시 아래 양식으로 추가:

```markdown
### ✅/❌ ISSUE-XXX — 이슈 제목

| 항목 | 내용 |
|------|------|
| **발생일** | YYYY-MM-DD |
| **해결일** | YYYY-MM-DD (미해결 시 '-') |
| **심각도** | 낮음 / 중간 / 높음 / 치명적 |
| **범주** | 환경설정 / 패키지설치 / 빌드 / 배포 / 기타 |

**증상:** ...
**원인:** ...
**해결 방법:** ...
```
