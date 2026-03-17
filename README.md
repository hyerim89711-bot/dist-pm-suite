# Distribution PM Suite v3 — 배포 & 연동 가이드

---

## 1단계. GitHub Pages 배포 (5분)

### 계정 없으면 먼저 가입
- github.com → Sign up → 무료 플랜 선택

### 저장소 만들기
1. github.com 로그인 후 우측 상단 **+** → **New repository**
2. Repository name: `dist-pm-suite` (원하는 이름)
3. **Public** 선택 (Pages 무료 사용 조건)
4. **Create repository** 클릭

### 파일 업로드
1. 저장소 페이지 → **Add file** → **Upload files**
2. `dist-pm-suite-v3.html` 파일을 드래그앤드롭
3. **⚠️ 파일명을 `index.html`로 바꿔야 합니다**
   - 업로드 창에서 파일명 클릭 → `index.html`로 수정
4. **Commit changes** 클릭

### Pages 활성화
1. 저장소 상단 탭 → **Settings**
2. 왼쪽 메뉴 → **Pages**
3. Source: **Deploy from a branch**
4. Branch: **main** / Folder: **/ (root)** 선택
5. **Save** 클릭
6. 1~2분 후 URL 생성: `https://[내아이디].github.io/dist-pm-suite/`

> ✅ 이 URL을 북마크하면 끝! 이후 파일 수정 시 같은 방법으로 업로드하면 자동 업데이트됩니다.

---

## 2단계. Google Sheets 백엔드 설정 (10분)

### 구글 시트 만들기
1. sheets.google.com → **새 스프레드시트 만들기**
2. 제목: `PM Suite DB` (아무 이름)

### Apps Script 코드 붙여넣기
1. 상단 메뉴 → **확장 프로그램** → **Apps Script**
2. 기존 코드(`function myFunction() {}`) 전체 삭제
3. PM Suite 앱 설정 페이지 → **"Apps Script 코드 복사하기"** 버튼 클릭
4. 복사된 코드를 Apps Script 창에 붙여넣기
5. **Ctrl+S** 저장 → 프로젝트 이름: `PM Suite Backend`

### 웹 앱으로 배포
1. 우측 상단 **배포** → **새 배포**
2. 톱니바퀴 아이콘 → **웹 앱** 선택
3. 설정:
   - 설명: `PM Suite v1`
   - 다음 사용자로 실행: **나** (내 계정)
   - 액세스 권한: **모든 사용자** ← ⚠️ 이게 핵심!
4. **배포** 클릭
5. **권한 승인** 팝업 → Google 계정 선택 → 고급 → "안전하지 않은 페이지로 이동" → 허용
6. **웹 앱 URL** 복사 (`https://script.google.com/macros/s/...` 형태)

### PM Suite에 URL 입력
1. PM Suite → **설정(⚙️)** 탭
2. **Apps Script Web App URL** 입력란에 붙여넣기
3. **연결 테스트** 버튼 클릭
4. "✅ Google Sheets 연결 성공!" 토스트 확인

> ✅ 이후 딜 등록/수정, MDF 활동 추가 시 구글 시트 자동 저장!

---

## 3단계. AI API 키 설정

### Claude (Anthropic) — 추천
1. console.anthropic.com 가입/로그인
2. 좌측 메뉴 → **API Keys** → **Create Key**
3. 키 복사 (`sk-ant-api03-...` 형태)
4. PM Suite → 설정 → AI API 설정 → **Claude (Anthropic)** 선택
5. API Key 입력란에 붙여넣기

### Gemini (Google) — 무료 옵션
1. aistudio.google.com → **Get API key** → **Create API key**
2. 키 복사 (`AIzaSy...` 형태)
3. PM Suite → 설정 → **Gemini (Google)** 선택
4. API Key 입력란에 붙여넣기

> API 키는 브라우저 localStorage에만 저장됩니다. 외부 서버로 전송되지 않습니다.

---

## 구글 시트 구조 (자동 생성됨)

| 시트명 | 내용 |
|--------|------|
| **Deals** | 딜 트래커 전체 목록 |
| **MDF** | MDF 예산 활동 목록 |
| **History** | 브리핑/제안서 저장 히스토리 |
| **Config** | MDF 벤더별 예산 설정 |

---

## 자주 쓰는 기능

| 기능 | 방법 |
|------|------|
| 시트에서 최신 데이터 불러오기 | 설정 → **⬇ 시트에서 불러오기** |
| 로컬→시트 전체 내보내기 | 설정 → **⬆ 전체 시트로 내보내기** |
| 앱 시작 시 자동 동기화 | GS URL 설정돼 있으면 자동 실행 |
| 전체 데이터 백업 | 설정 → **전체 데이터 내보내기 (JSON)** |
| 앱 초기화 | 설정 → **전체 초기화** |

---

## 파일 업데이트 방법

앱을 수정하고 싶을 때:
1. GitHub 저장소 → `index.html` 클릭
2. 우측 상단 연필 아이콘(Edit) → 기존 내용 전체 삭제 → 새 내용 붙여넣기
3. **Commit changes** → 1~2분 후 자동 반영

또는 **Add file → Upload files**로 같은 이름(`index.html`)으로 덮어쓰기.
