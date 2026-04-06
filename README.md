# JSX Renderer

Claude.ai에서 다운로드한 `.jsx` 파일(Artifact)을 모바일에서 바로 열어볼 수 있는 웹앱입니다.

---

## 사용 방법

### 1. 앱 열기
- 모바일 브라우저에서 접속: **https://dkmin7545.github.io/jsx-renderer/**
- "홈 화면에 추가"하면 일반 앱처럼 사용할 수 있습니다

### 2. JSX 파일 렌더링
1. Claude.ai에서 Artifact를 다운로드합니다 (`.jsx` 파일)
2. 앱에서 "파일 선택" 버튼을 탭합니다
3. 다운로드된 `.jsx` 파일을 선택합니다
4. 즉시 화면에 렌더링됩니다

### 3. 최근 파일
- 한번 열었던 파일은 "최근 파일" 목록에 저장됩니다
- 다시 열고 싶으면 목록에서 탭하면 됩니다

---

## 지원하는 라이브러리

Claude가 Artifact에서 자주 사용하는 라이브러리들을 지원합니다:

| 라이브러리 | 용도 |
|-----------|------|
| React | UI 렌더링 (기본) |
| Tailwind CSS | 스타일링 |
| Recharts | 차트/그래프 |
| Lucide React | 아이콘 |
| Framer Motion | 애니메이션 |
| Lodash | 유틸리티 함수 |
| date-fns | 날짜 처리 |
| PapaParse | CSV 파싱 |

---

## 기술 구성

- **단일 HTML 파일** — 서버 없이 브라우저만으로 동작
- **PWA (Progressive Web App)** — 홈 화면에 추가하면 앱처럼 동작하고, 핵심 파일을 캐싱하여 빠르게 로드
- **브라우저 내 변환** — Babel을 사용해 JSX 코드를 브라우저에서 직접 변환하여 실행

### 파일 구조
```
jsx-renderer/
├── index.html       ← 앱 본체
├── manifest.json    ← PWA 설정 (앱 이름, 아이콘, 테마 등)
├── sw.js            ← Service Worker (오프라인 캐싱)
├── icon-192.png     ← 홈 화면 아이콘 (작은 크기)
└── icon-512.png     ← 홈 화면 아이콘 (큰 크기)
```

---

## GitHub Pages 배포 과정 기록

이 앱은 GitHub Pages를 통해 인터넷에 공개되어 있습니다.
아래는 배포까지 진행한 작업을 순서대로 정리한 것입니다.

### 1단계: GitHub 저장소(레포지토리) 만들기

GitHub 웹사이트에서 `jsx-renderer`라는 이름의 새 저장소를 만들었습니다.
저장소는 코드를 보관하고 관리하는 공간입니다. "Public(공개)"으로 설정해야 GitHub Pages를 무료로 사용할 수 있습니다.

- 주소: https://github.com/dkmin7545/jsx-renderer

### 2단계: GitHub CLI(gh) 설치

터미널(명령줄)에서 GitHub에 코드를 올리려면 인증이 필요합니다.
`gh`라는 GitHub 공식 도구를 설치하여 이 인증을 처리했습니다.

```bash
brew install gh        # macOS용 패키지 관리자(Homebrew)로 설치
gh auth login --web    # 브라우저에서 GitHub 계정 로그인
```

로그인 과정에서 일회용 코드가 표시되고, 브라우저에서 해당 코드를 입력하면 인증이 완료됩니다.

### 3단계: 코드를 GitHub에 업로드(push)

로컬 컴퓨터에 있는 앱 파일들을 GitHub 저장소에 올렸습니다.

```bash
git init                          # 이 폴더를 git으로 관리하기 시작
git add index.html manifest.json sw.js icon-192.png icon-512.png  # 올릴 파일 선택
git commit -m "Initial commit"    # 변경사항을 하나의 묶음(커밋)으로 저장
git remote add origin https://github.com/dkmin7545/jsx-renderer.git  # GitHub 저장소 연결
gh auth setup-git                 # git이 GitHub 인증을 사용하도록 설정
git push -u origin main           # GitHub에 업로드
```

### 4단계: GitHub Pages 활성화

GitHub Pages는 저장소에 올린 파일을 웹사이트로 자동 공개해주는 기능입니다.
GitHub API를 통해 이 기능을 켰습니다.

```bash
# Pages를 main 브랜치의 루트(/) 경로에서 배포하도록 설정
gh api repos/dkmin7545/jsx-renderer/pages -X PUT \
  -f build_type=legacy -f source.branch=main -f source.path=/
```

이렇게 하면 GitHub가 자동으로 웹사이트를 생성합니다:
- **결과 주소**: https://dkmin7545.github.io/jsx-renderer/

### 이후 코드를 수정하면?

코드를 수정한 후 다시 GitHub에 올리면 웹사이트도 자동으로 업데이트됩니다:

```bash
git add .
git commit -m "변경 내용 설명"
git push
```

1~2분 후 반영됩니다.
