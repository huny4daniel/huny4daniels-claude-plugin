# huny4daniels-claude-plugin

개인 Claude Code 플러그인 마켓플레이스.

| 플러그인 | 명령 | 용도 |
|---|---|---|
| project-process | `/adopt [템플릿 경로]` | [huny4daniels-TEMPLATE](https://github.com/huny4daniel/huny4daniels-TEMPLATE)의 구조와 진행 절차를 현재 폴더에 적용. 빈 폴더면 새 프로젝트로 시작(`/kickoff`로 이어짐), 기존 프로젝트면 덮어쓰지 않고 단계적으로 도입, 이미 적용된 프로젝트면 템플릿 업데이트 반영(`.template-version` 기준) |

템플릿 자체(폴더 구조·문서·프로젝트 명령)는 템플릿 저장소에만 둔다. 이 플러그인은 그것을 가져와 적용하는 명령만 담는다.

## 설치 (컴퓨터마다 한 번)

비공개 저장소이므로 그 컴퓨터에서 GitHub 인증(`gh auth login`)이 되어 있어야 한다.

```
/plugin marketplace add huny4daniel/huny4daniels-claude-plugin
/plugin install project-process@huny4daniels
```

또는 터미널에서:

```bash
claude plugin marketplace add huny4daniel/huny4daniels-claude-plugin
claude plugin install project-process@huny4daniels
```

## 업데이트

명령을 고쳐 push한 뒤 `plugin.json`의 `version`을 올리고, 각 컴퓨터에서:

```bash
claude plugin marketplace update huny4daniels
claude plugin update project-process@huny4daniels
```
