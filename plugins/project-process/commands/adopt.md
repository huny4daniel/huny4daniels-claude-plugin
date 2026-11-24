---
description: 표준 모노레포 템플릿의 구조와 진행 절차를 현재 폴더에 적용 (빈 폴더면 새로 시작, 기존 프로젝트면 단계적 도입)
argument-hint: [템플릿 경로, 생략 시 GitHub 템플릿 저장소 사용]
---

템플릿: $ARGUMENTS

현재 폴더에 템플릿(huny4daniel/huny4daniels-TEMPLATE)의 구조와 진행 체계를 적용한다. 템플릿의 docs/PROCESS.md 협업 규칙을 따르고, 응답은 [질문] / [제안] / [승인 요청] / [요청] 중 하나로 끝낸다.

## 0. 준비

- 템플릿 경로가 없으면 `gh repo clone huny4daniel/huny4daniels-TEMPLATE`로 현재 폴더 밖의 임시 폴더에 받는다. clone이 실패하면 `gh auth login` 여부를 확인하도록 [요청]한다.
- 현재 폴더 상태를 확인해 **모드**를 정한다:
  - **새 프로젝트 모드**: git 저장소가 아니거나 커밋이 없고, 소스 코드·빌드 설정 파일이 없다 (README, LICENSE, .gitignore, .git 정도만 있는 것은 빈 폴더로 본다).
  - **도입 모드**: 그 외 (코드나 커밋 이력이 있다).
- 판단 근거와 모드를 한 줄로 알리고 진행한다. 애매하면 [질문]한다.

## A. 새 프로젝트 모드

1. 프로젝트 이름을 [질문]한다 (기본값: 현재 폴더 이름).
2. 템플릿의 `.git`과 `tools/scripts/new-project.ps1`을 제외한 모든 파일·폴더를 복사한다. 이미 있는 파일(README, LICENSE, .gitignore 등)은 덮어쓰지 않고:
   - README: 기존 내용을 템플릿 README 형식으로 옮겨 합친다.
   - .gitignore: 빠진 항목만 추가한다.
   - LICENSE: 그대로 둔다.
3. `.md` 파일의 `{{PROJECT_NAME}}`, `{{제품 이름}}`을 프로젝트 이름으로 바꾼다. 나머지 자리표시자는 그대로 둔다.
4. git 저장소가 아니면 `git init -b main`. 첫 커밋을 [승인 요청]한다 (사용자의 커밋 메시지 규칙을 따른다).
5. 원격 저장소가 없으면 만들지 여부를 [질문]한다 (`gh repo create <이름> --private --source . --push`).
6. 임시 템플릿 폴더를 삭제하고, 템플릿의 `.claude/commands/kickoff.md` 절차로 바로 이어간다 (아이디어를 [질문]). 새 세션에서 `/kickoff`를 써도 된다고 안내한다.

## B. 도입 모드

1. **사전 점검**
   - `git status`가 깨끗한지 확인한다. 커밋되지 않은 변경이 있으면 먼저 정리할지 [질문]한다.
   - 작업 브랜치(`docs/adopt-process`)를 만들어 진행할 것을 제안한다.
2. **현황 파악** — README, 기존 CLAUDE.md/AGENTS.md, 빌드 설정, CI·릴리즈 워크플로, 폴더 구조, 최근 git 이력, 열린 GitHub 이슈를 읽고 한 화면으로 요약한다.
3. **비침습 추가** — 아래 원칙으로 추가·병합할 목록을 보여주고 [승인 요청]한 뒤 적용한다.
   - 없는 파일만 복사: AGENTS.md, docs/ 전체, `.claude/commands/`, `.claude/hooks/`, `.github/ISSUE_TEMPLATE/`, `.github/pull_request_template.md`, CHANGELOG.md, CONTRIBUTING.md, .editorconfig, .env.example
   - 기존 파일은 덮어쓰지 않고 병합:
     - CLAUDE.md: 기존 내용 유지 + 템플릿 CLAUDE.md의 import(`@AGENTS.md`, `@docs/PROCESS.md`, `@docs/STATUS.md`)와 진행 규칙 추가. 기존 CLAUDE.md의 프로젝트 정보 중 AGENTS.md 성격(구조, 명령어, 규칙)인 것은 AGENTS.md로 옮길지 [제안]한다.
     - AGENTS.md가 이미 있으면 템플릿 항목 중 빠진 섹션만 추가한다.
     - .gitignore·.gitattributes: 빠진 항목만. `.claude/settings.json`: 권한과 `hooks`를 합친다 (기존 훅은 유지하고 템플릿의 PreToolUse 훅을 추가). 프로젝트의 기본 브랜치가 main/master가 아니면 그 사실을 알린다.
   - 건드리지 않음: 소스 코드, 빌드 설정, 기존 CI·release 워크플로, README 본문
   - `apps/`, `packages/`, `tools/` 폴더는 만들지 않는다. 코드 이동은 하지 않는다.
4. **역방향 문서화** — 코드를 근거로 초안을 쓰고 문서마다 확인을 받는다.
   - AGENTS.md: 실제 스택·명령어(설치, 실행, 테스트, 빌드)를 채운다. 명령은 실제로 실행해 확인한다.
   - docs/architecture/overview.md: 현재 구조와 주요 흐름
   - docs/adr/: 이미 내린 주요 결정을 사후 기록(맥락에 "사후 기록" 명시). 대상 목록을 먼저 보여주고 고르게 한다.
   - docs/product/PRD.md: 현재 기능 목록 중심. 목표·비목표는 [질문]으로 확인한다.
5. **현재 위치 결정** — docs/STATUS.md에 단계·모드를 제안해 [승인 요청]한다. 0~2단계는 역방향 문서로 완료 처리하고, 열린 이슈가 대부분 버그면 유지보수 모드, 계획된 기능이 있으면 개발 모드(3 또는 4단계)로 둔다. 도입 내용을 세션 로그와 결정 기록에 남긴다.
6. **마무리** — 변경 요약을 보여주고 커밋을 [승인 요청]한다. 폴더 구조 변경은 필요해질 때 ADR과 함께 별도 작업으로 하자고 안내한다. 임시 템플릿 폴더를 삭제한다.
