# Back-End

웹 취약점 분석 실습 플랫폼의 NestJS 백엔드 프로젝트입니다.


## 1. 기술 스택

| 구분 | 기술 |
| --- | --- |
| Runtime | Node.js 24 LTS |
| Backend | NestJS 11 |
| Language | TypeScript |
| Package Manager | npm |
| ORM | Prisma — 구성 예정 |
| Database | PostgreSQL — 구성 예정 |
| Infrastructure | Docker Desktop / Docker Compose — 구성 예정 |
| Frontend | Next.js App Router + React + TypeScript — 별도 저장소 |
| Version Control | Git / GitHub |
| Security Testing | Burp Suite / Chrome DevTools |


## 2. Windows 설치 체크리스트

처음 환경을 구성한다면 아래 순서로 진행합니다.

현재 백엔드 실행에는 VS Code, Node.js, Git이 필요합니다. WSL 2와 Docker는 이후 컨테이너 환경 구성에, Burp Suite는 취약점 점검에 사용합니다.

- [ ] VS Code 설치
- [ ] Node.js 24 LTS 설치
- [ ] Git for Windows 설치
- [ ] WSL 2 설치 — Docker 사용 준비
- [ ] Docker Desktop 설치 — 컨테이너 사용 준비
- [ ] Burp Suite 설치 — 수동 점검 준비

### 2.1 VS Code

코드 편집, 프로젝트 관리, 터미널 실행에 사용합니다.

[VS Code 공식 다운로드](https://code.visualstudio.com/download)


### 2.2 Node.js 24 LTS

NestJS와 npm을 실행하기 위해 필요합니다.

[Node.js 공식 다운로드](https://nodejs.org/en/download)

1. 버전은 **24.x LTS**를 선택합니다.
2. Windows용 Installer (`.msi`)를 다운로드합니다.
3. PC 아키텍처에 맞는 설치 파일로 설치합니다.
4. 설치 후 VS Code를 완전히 종료했다가 다시 실행합니다.
5. 새 터미널에서 확인합니다.

```powershell
node -v
npm -v
```

확인 기준:

- `node -v`: `v24.`로 시작하는 버전
- `npm -v`: npm 버전 출력

npm은 Node.js와 함께 설치되므로 별도로 설치할 필요가 없습니다.

### 2.3 Git for Windows

GitHub 저장소 다운로드와 변경 사항 관리에 사용합니다.

[Git for Windows 공식 설치 안내](https://git-scm.com/install/windows)

### 2.4 WSL 2

Docker의 WSL 2 백엔드를 사용할 때 필요한 환경입니다.

[Microsoft 공식 WSL 설치 안내](https://learn.microsoft.com/en-us/windows/wsl/install)

**관리자 권한 PowerShell**에서 실행합니다.

```powershell
wsl --install
```

설치 안내에 따라 PC를 재시작합니다. 배포판 최초 실행 시 사용자 계정을 설정합니다.

설치 후 상태를 확인합니다.

```powershell
wsl --update
wsl --status
wsl --list --verbose
```

배포판 목록의 `VERSION`이 `2`인지 확인합니다.

이미 WSL이 설치되어 있다면 재설치하기보다 현재 상태와 업데이트 여부부터 확인합니다.

### 2.5 Docker Desktop

PostgreSQL과 별도 실습 컨테이너를 실행하는 데 사용할 예정입니다.

[Docker Desktop Windows 공식 설치 안내](https://docs.docker.com/desktop/setup/install/windows-install/)

1. 공식 문서에서 Windows 버전, 가상화 지원 등 시스템 요구사항을 확인합니다.
2. PC에 맞는 Docker Desktop을 설치합니다.
3. WSL 2 백엔드를 사용하는 Linux 컨테이너 환경으로 구성합니다.
4. Docker Desktop 앱을 실행하고 엔진이 준비될 때까지 기다립니다.

일반 PowerShell에서 확인합니다.

```powershell
docker --version
docker compose version
docker info
```

앞의 두 명령은 CLI 버전을 확인합니다. `docker info`까지 서버 정보를 반환하면 Docker 엔진에 연결된 것입니다.

> 현재 저장소에는 Docker Compose 파일이 없습니다. 아직 `docker compose up`을 실행하지 않습니다.

## 4. 따로 설치하지 않는 항목

| 항목 | 설치·관리 방법 |
| --- | --- |
| npm | Node.js 설치 시 함께 제공 |
| NestJS | 백엔드에서 `npm ci` 실행 시 설치 |
| TypeScript | 백엔드에서 `npm ci` 실행 시 설치 |
| Nest CLI | 프로젝트 개발 의존성 사용 |
| Next.js / React | 프론트엔드 저장소에서 설치 |
| Prisma | 백엔드 의존성에 추가한 뒤 npm으로 설치 |
| PostgreSQL | Docker 구성 후 컨테이너로 실행 |

팀원은 백엔드를 실행하기 위해 Nest CLI를 전역 설치할 필요가 없습니다.

프로젝트를 새로 만드는 `nest new`나 `git init`도 실행하지 않습니다. 이미 만들어진 GitHub 저장소를 Clone해서 사용합니다.

## 5. GitHub에서 프로젝트 다운로드

저장소:

[4184LAB / Back-End](https://github.com/4184LAB/Back-End)



### Windows PowerShell

소스를 저장할 상위 폴더에서 실행합니다. 아래 예시는 사용자 홈에 `Back-End` 폴더를 생성합니다.

```powershell
cd $HOME
git clone https://github.com/4184LAB/Back-End.git
cd Back-End
```

### macOS

```bash
cd ~/Desktop
git clone https://github.com/4184LAB/Back-End.git
cd Back-End
```

이미 Clone한 폴더가 있다면 다시 다운로드하지 말고 해당 폴더를 엽니다.

VS Code의 **파일 → 폴더 열기**에서 `Back-End` 폴더를 선택합니다.

`code` 명령이 설정되어 있다면 다음 명령으로 열어도 됩니다.

```bash
code .
```

### 저장소 위치 확인

```bash
git rev-parse --show-toplevel
git remote -v
```

원격 주소가 다음과 같은지 확인합니다.

```text
https://github.com/4184LAB/Back-End.git
```

이 저장소는 최상위 폴더 자체가 백엔드 프로젝트입니다.

Clone 후 `cd Back-End`로 이동했다면 그 안에서 다시 `cd backend`를 실행하지 않습니다.

## 6. 의존성 설치

`package.json`과 `package-lock.json`이 있는 폴더에서 실행합니다.

Windows와 macOS 모두 동일합니다.

```bash
npm ci
```

`npm ci`는 `package-lock.json`에 기록된 버전 조합으로 의존성을 설치합니다.

- 기존 `node_modules`가 있으면 교체합니다.
- 잠금 파일을 임의로 갱신하지 않습니다.
- Mac의 `node_modules`를 Windows로 복사하지 않습니다.
- 각 PC에서 직접 설치합니다.

새로운 패키지를 개발 목적으로 추가할 때에는 다음 명령을 사용합니다.

```bash
npm install 패키지명
```

이때 변경된 `package.json`과 `package-lock.json`은 함께 커밋합니다.

## 7. 개발 서버 실행

프론트엔드와 포트가 충돌하지 않도록 다음 기준으로 실행합니다.

| 구분 | 포트 |
| --- | --- |
| 프론트엔드 | 3001 |
| 백엔드 | 3000 |

현재 백엔드 코드의 기본 포트는 `3000`입니다.

### Windows PowerShell

```powershell
npm run start:dev
```

## 8. 프론트엔드 개발자 안내

프론트엔드 개발자는 이 백엔드 저장소도 별도로 Clone하고 실행합니다.

개발 중에는 각자의 PC에서 프론트엔드와 백엔드를 함께 실행합니다. `localhost`는 본인 PC를 의미합니다.

| 항목 | 개발 주소 |
| --- | --- |
| 프론트엔드 | `http://localhost:3001` |
| 백엔드 | `http://localhost:3000` |
| 현재 실행 확인 API | `GET http://localhost:3000/` |
| 현재 응답 | 일반 문자열 `Hello World!` |

현재 응답은 JSON이 아닙니다.

## 9. 백엔드 환경변수


## 10. 프로젝트 구조

```text
Back-End/
├── src/
│   ├── main.ts
│   ├── app.module.ts
│   ├── app.controller.ts
│   ├── app.service.ts
│   └── app.controller.spec.ts
├── .gitignore
├── .prettierrc
├── eslint.config.mjs
├── nest-cli.json
├── package.json
├── package-lock.json
├── tsconfig.json
├── tsconfig.build.json
└── README.md
```

| 파일·폴더 | 역할 |
| --- | --- |
| `src/main.ts` | 서버 시작과 포트 설정 |
| `src/app.module.ts` | 최상위 Nest 모듈 |
| `src/app.controller.ts` | `GET /` 요청 처리 |
| `src/app.service.ts` | `Hello World!` 반환 |
| `src/app.controller.spec.ts` | 기본 단위 테스트 |
| `package.json` | 의존성과 실행 스크립트 |
| `package-lock.json` | 설치할 의존성 버전 고정 |
| `.gitignore` | Git 추적 제외 설정 |
| `node_modules/` | 의존성 설치 시 생성, Git 제외 |
| `dist/` | 빌드 시 생성, Git 제외 |

## 11. 주요 명령어

모든 명령은 `package.json`이 있는 프로젝트 최상위 폴더에서 실행합니다.

| 명령어 | 설명 |
| --- | --- |
| `npm ci` | 잠금 파일 기준 의존성 설치 |
| `npm run start:dev` | 변경 감지 개발 서버 실행 |
| `npm run start` | 기본 서버 실행 |
| `npm run build` | 프로젝트 빌드 |
| `npm run start:prod` | 빌드된 서버 실행 |
| `npm test` | 단위 테스트 실행 |
| `npm run test:watch` | 변경 감지 단위 테스트 |
| `npm run test:cov` | 테스트 커버리지 확인 |
| `npm run lint` | ESLint 검사 및 자동 수정 |
| `npm run format` | Prettier 포맷 적용 |


## 12. 최신 코드 받기

작업 전 현재 저장소와 변경 사항을 확인합니다.

```bash
git remote -v
git status
```

작업 중인 변경 사항은 먼저 커밋하거나 별도로 보관합니다.

```bash
git switch main
git pull --ff-only origin main
```

`package-lock.json`이 변경되었다면 의존성을 다시 설치합니다.

```bash
npm ci
```

공동 개발은 기능별 브랜치에서 진행하고 Pull Request로 변경 내용을 공유합니다.

Pull에 실패하면 로컬 변경 사항과 커밋 차이를 확인합니다. 강제 Push로 해결하지 않습니다.

## 13. Mac·Windows 협업 시 주의사항

- 소스는 GitHub의 Push / Pull로 공유합니다.
- Node.js는 팀 기준인 24.x로 맞춥니다.
- `node_modules`와 `dist`는 운영체제 간 복사하지 않습니다.
- 각 PC에서 `npm ci`와 빌드를 실행합니다.
- 실제 `.env`는 Git에 올리지 않습니다.
- `.DS_Store`, `coverage` 등 생성 파일은 커밋하지 않습니다.
- 파일명과 import 경로의 대소문자를 정확히 맞춥니다.
- 사용자별 절대 경로를 코드에 고정하지 않습니다.
- Prisma 도입 후에는 각 실행 환경에서 Client를 생성합니다.
- PostgreSQL 데이터와 Docker 볼륨은 Git 소스와 별도로 관리합니다.
- PowerShell과 macOS의 환경변수 설정 문법을 구분합니다.
- Windows PowerShell과 WSL의 Node 실행 환경을 섞지 않습니다.

