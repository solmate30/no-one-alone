# AGENTS.md — no-one-alone
> Created: 2026-05-08 17:45
> Last Updated: 2026-05-08 17:45
> Backlog: D-01

## 1. Purpose

This file defines the shared rules for all AI agents working in this repository. Agent-specific files such as `CLAUDE.md` may add tool-specific guidance, but they must not override the project rules in this file.

Project name: `no-one-alone` / Solmate

Core message:

> 국가가 못 찾는 사람을, 이웃이 찾고, AI가 연결하고, 블록체인이 증명한다.

Current state:

- The project is in the proposal and documentation phase.
- No application code exists yet.
- The immediate target is the 2026-05-31 proposal submission.
- If the team advances, the finals MVP implementation period is 2026-07-01 to 2026-09-21.

## 2. Docs-First Rule

Documentation is the source of truth. Do not implement a feature before the relevant documents exist and are connected to the backlog.

Before creating or editing code, confirm that the feature is covered by:

- [Product Specs](./docs/01_Concept_Design/03_PRODUCT_SPECS.md)
- [Screen Flow](./docs/02_UI_Screens/00_SCREEN_FLOW.md)
- [UI Design](./docs/02_UI_Screens/01_UI_DESIGN.md)
- [DB Schema](./docs/03_Technical_Specs/01_DB_SCHEMA.md)
- [API Specs](./docs/03_Technical_Specs/02_API_SPECS.md)
- [Backlog](./docs/04_Logic_Progress/00_BACKLOG.md)
- [QA Checklist](./docs/05_QA_Validation/02_QA_CHECKLIST.md)

If any of these are missing or incomplete, update the documents first.

## 3. Backlog Linking Rule

All work must connect to a backlog ID in [00_BACKLOG.md](./docs/04_Logic_Progress/00_BACKLOG.md).

Backlog ID prefixes:

| Prefix | Meaning |
|:---|:---|
| `P-*` | Proposal writing tasks |
| `D-*` | Document and design system tasks |
| `T-*` | Technical research and specification tasks |
| `M-*` | Finals MVP implementation tasks |
| `Q-*` | QA, validation, and presentation tasks |

When creating or updating a document:

1. Add or update the document's `> Backlog:` metadata.
2. Add or update the document's `Related Documents` section.
3. Add the document to [Document Index](./docs/00_DOCUMENT_INDEX.md).
4. Ensure the related task card in [Backlog](./docs/04_Logic_Progress/00_BACKLOG.md) lists the document under `필수 참조` or `생성/업데이트 문서`.

## 4. Required Document Metadata

Every shared Markdown document should start with:

```markdown
# [Document Title]
> Created: YYYY-MM-DD HH:mm
> Last Updated: YYYY-MM-DD HH:mm
> Backlog: P-01, D-01
```

Update `Last Updated` whenever a document changes.

Use `> Backlog: 전체` only for documents that govern the full project, such as the central backlog.

## 5. 5-Layer Documentation System

The repository uses a 5-layer documentation structure:

| Layer | Path | Purpose |
|:---|:---|:---|
| Concept Design | `docs/01_Concept_Design/` | Vision, business model, MVP scope, proposal deck |
| UI Screens | `docs/02_UI_Screens/` | User flows, screen structure, UI design rules |
| Technical Specs | `docs/03_Technical_Specs/` | Development principles, DB schema, API contracts |
| Logic Progress | `docs/04_Logic_Progress/` | Backlog, roadmap, execution planning |
| QA Validation | `docs/05_QA_Validation/` | Test scenarios, QA checklist, submission validation |

Higher-layer changes must propagate downward. For example, if MVP scope changes in Product Specs, update Screen Flow, API Specs, Backlog, and QA documents as needed.

## 6. Collaboration and Approval

This project follows an explicit discussion-first workflow.

- Do not start implementation from vague instructions.
- Before code or substantial document edits, state the purpose and expected files.
- Ask clarifying questions when the backlog ID, scope, or source document is unclear.
- Do not mark a phase complete unless the user agrees it is complete.
- For implementation work, get explicit approval after the planning and pre-code verification steps.
- Do not use emojis in project documentation or agent-facing project files.

## 7. Git Workflow

Branch strategy:

```text
main          — stable submission/deployment branch
develop       — integration branch
docs/*        — documentation work
feat/*        — feature implementation
fix/*         — bug fixes
```

Current preferred flow:

```text
feature/docs branch -> develop -> main
```

Commit format:

```text
docs(backlog): 백로그 문서 연결 체계 정리

- 작업 ID 기반 백로그 구조 추가
- 문서별 Backlog 메타데이터 연결
- Document Index 추가
```

Allowed commit types:

```text
feat / fix / chore / docs / refactor / test
```

## 8. Implementation Gate

Before writing code for any MVP feature, verify:

- The feature is in the finals MVP scope.
- The relevant user flow exists.
- The UI requirements are documented.
- The DB tables and API endpoints are defined.
- The backlog card lists required references and completion criteria.
- QA or test criteria exist.

If the answer is no for any item, stop and update the documents first.

## 9. Files and Scope

Shared project assets:

- `docs/**`
- `AGENTS.md`
- `CLAUDE.md`
- `solmate_hackathon_proposal.md`
- `refs/**` as read-only reference material

Do not casually edit:

- Generated files
- Local IDE settings
- Local-only agent skill folders
- Secrets or environment files

When unrelated untracked or modified files are present, do not delete or revert them unless the user explicitly asks.

## 10. Related Documents

- **Documentation**: [Document Index](./docs/00_DOCUMENT_INDEX.md) — full map of documents and backlog IDs
- **Logic_Progress**: [Backlog](./docs/04_Logic_Progress/00_BACKLOG.md) — authoritative task list and work hub
- **Technical_Specs**: [Development Principles](./docs/03_Technical_Specs/00_DEVELOPMENT_PRINCIPLES.md) — coding, branch, security, and performance principles
- **QA_Validation**: [QA Checklist](./docs/05_QA_Validation/02_QA_CHECKLIST.md) — proposal and implementation validation checklist
