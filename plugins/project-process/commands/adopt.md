---
description: 이미 진행 중인 프로젝트에 표준 구조와 진행 절차를 도입
argument-hint: [템플릿 경로, 생략 시 GitHub 템플릿 저장소 사용]
---

템플릿: $ARGUMENTS

현재 폴더(기존 프로젝트)에 템플릿의 문서·진행 체계를 단계적으로 도입한다. 템플릿의 docs/PROCESS.md "기존 프로젝트에 도입" 절을 따른다.

0. **준비**
   - 템플릿 경로가 없으면 `gh repo clone huny4daniel/huny4daniels-TEMPLATE`로 임시 폴더(작업 폴더 밖)에 받는다.
   - `git status`가 깨끗한지 확인한다. 커밋되지 않은 변경이 있으면 먼저 정리할지 [질문]한다.
   - 작업 브랜치(`docs/adopt-process`)를 만들어 진행할 것을 제안한다.
1. **현황 파악** — README, 기존 CLAUDE.md/AGENTS.md, 빌드 설정, CI·릴리즈 워크플로, 폴더 구조, 최근 git 이력, 열린 GitHub 이슈를 읽고 한 화면으로 요약한다.
2. **비침습 추가** — 아래 원칙으로 무엇을 추가·병합할지 목록을 보여주고 [승인 요청]한 뒤 적용한다.
   - 없는 파일만 복사: docs/ 전체, `.claude/commands/`, `.github/ISSUE_TEMPLATE/`, `.github/pull_request_template.md`, CHANGELOG.md, CONTRIBUTING.md, .editorconfig
   - 기존 파일은 덮어쓰지 않고 병합: CLAUDE.md(기존 내용 유지 + 템플릿 CLAUDE.md의 import와 진행 규칙 추가), .gitignore·.gitattributes(빠진 항목만), `.claude/settings.json`(권한 합치기)
   - 건드리지 않음: 소스 코드, 빌드 설정, 기존 CI·release 워크플로, README 본문
   - `apps/`, `packages/`, `tools/` 폴더는 만들지 않는다. 코드 이동은 하지 않는다.
3. **역방향 문서화** — 코드를 근거로 초안을 쓰고 문서마다 확인을 받는다.
   - AGENTS.md: 실제 스택·명령어(설치, 실행, 테스트, 빌드)를 채운다. 명령은 실제로 실행해 확인한다.
   - docs/architecture/overview.md: 현재 구조와 주요 흐름
   - docs/adr/: 이미 내린 주요 결정을 사후 기록(맥락에 "사후 기록" 명시). 대상 목록을 먼저 보여주고 고르게 한다.
   - docs/product/PRD.md: 현재 기능 목록 중심. 목표·비목표는 [질문]으로 확인한다.
4. **현재 위치 결정** — docs/STATUS.md에 단계·모드를 제안해 [승인 요청]한다. 0~2단계는 역방향 문서로 완료 처리하고, 열린 이슈가 대부분 버그면 유지보수 모드, 계획된 기능이 있으면 개발 모드(3 또는 4단계)로 둔다. 도입 내용을 세션 로그와 결정 기록에 남긴다.
5. **마무리** — 변경 요약을 보여주고 커밋을 [승인 요청]한다. 폴더 구조 변경은 필요해질 때 ADR과 함께 별도 작업으로 하자고 안내한다. 임시로 받은 템플릿 폴더는 삭제한다.
