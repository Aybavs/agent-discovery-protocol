# Contributing

Thank you for your interest in Agent Discovery Protocol.

This project is currently in an early working-draft phase. The most valuable contributions are careful feedback, scope review, prior-art analysis, security review, and terminology improvements.

## Current project phase

The current focus is:

1. refining the problem statement,
2. clarifying the relationship to existing standards,
3. collecting use cases,
4. identifying security considerations,
5. preparing the first technical specification outline.

Large implementation work should wait until the discovery model is more stable.

## How to contribute

You can contribute by:

- opening an issue,
- starting a discussion,
- suggesting wording improvements,
- identifying related standards or prior work,
- proposing use cases,
- reviewing security implications,
- improving examples,
- improving translations.

## Branch workflow

This project uses a lightweight GitHub Flow model.

- `main` is the only long-lived branch and represents the current public working draft.
- Changes should be made in short-lived topic branches and proposed through pull requests.
- Contributors without write access should create a fork and open a pull request from a branch in that fork.
- Maintainers with write access may create topic branches directly in the upstream repository.
- Direct pushes to `main` are not part of the normal contribution workflow.
- Topic branches should be deleted after they are merged.

Branch names should be lowercase, concise, and describe the change. For example:

```text
docs/rfc-0001-media-type
docs/rfc-0000-clarify-a2a
chore/add-markdown-lint
```

The project does not use long-lived `develop`, release, or document-specific branches.

## Before proposing a large change

For major changes, please open an issue or discussion first.

Examples of major changes include:

- changing project terminology,
- changing the scope,
- adding a new discovery requirement,
- proposing a concrete endpoint name,
- proposing a schema structure,
- adding a new document to the RFC series.

This helps keep the project focused.

## Writing style

Please follow these principles:

- Use clear and neutral language.
- Do not frame existing standards as failures.
- Explain which problem a mechanism solves before explaining what remains outside its scope.
- Avoid vendor-specific assumptions.
- Avoid hype.
- Prefer small, testable claims.
- Separate problem statements from solutions.
- Separate discovery from authorization, trust, pricing, policy, and capability semantics.

## Relationship to existing standards

This project should not be positioned as a replacement for existing standards.

When discussing existing mechanisms such as OpenAPI, MCP, A2A, OAuth, `security.txt`, `robots.txt`, `sitemap.xml`, OpenID Discovery, or `llms.txt`, use neutral language.

Preferred phrasing:

```text
This mechanism solves a different problem.
```

Avoid phrasing such as:

```text
This mechanism is insufficient.
This mechanism is obsolete.
This mechanism is wrong.
```

## Document naming

Use lowercase file names with hyphens.

Good:

```text
rfc-0000-problem-statement.md
rfc-0001-agent-discovery-protocol.md
rfc-0002-rationale-and-design-decisions.md
```

Avoid:

```text
RFC-0000-Problem-Statement(1).md
My Document.md
Türkçe Belge.md
```

## Commit messages

This project follows [Conventional Commits](https://www.conventionalcommits.org/).

Format:

```text
<type>[(scope)]: <short description>
```

Common types:

| Type | Use when |
|---|---|
| `docs` | Changing document content (RFCs, translations, manifesto) |
| `feat` | Adding a new feature or requirement |
| `fix` | Correcting an error or inconsistency |
| `chore` | Repository maintenance, tooling, CI, templates |
| `refactor` | Restructuring without changing meaning |
| `style` | Formatting, whitespace, punctuation (no content change) |

Optional scopes: `rfc-0000`, `rfc-0001`, `rfc-0002`, `schema`, `examples`, `i18n`.

Good:

```text
docs(rfc-0000): clarify A2A scope in gap analysis
docs(rfc-0000): add semantic injection security considerations
feat(rfc-0000): add operator control requirement
chore: add GitHub issue templates
docs(i18n): sync Turkish translation with latest English draft
```

Avoid:

```text
update
fix
new
changes
```

## Pull requests

A pull request should explain:

- what changed,
- why it changed,
- which document section it affects,
- whether it changes scope,
- whether it introduces a new requirement.

The `main` branch should be protected against deletion and force pushes. Pull requests should target `main`, all review conversations should be resolved before merge, and pull requests should be squash-merged to keep the history linear. While the project has one active maintainer, a second approval is not required. If another active maintainer joins, at least one approving review should be required for changes to `main`.

## Release versioning

Repository releases are tagged from `main`. The project does not maintain separate release branches.

During the working-draft phase, releases use [Semantic Versioning](https://semver.org/) in the `0.y.z` range:

- `v0.1.0` will mark the first coherent and implementable RFC-0001 working draft.
- A minor release, such as `v0.2.0`, indicates a change to the discovery model, normative processing rules, or conformance requirements.
- A patch release, such as `v0.1.1`, is reserved for editorial corrections and other changes that do not alter normative behavior.
- Breaking changes may occur before `v1.0.0` and must be documented in the release notes.
- `v1.0.0` will require a stable core specification informed by implementation experience; document completion alone is not sufficient.

RFC identifiers such as `RFC-0000` and `RFC-0001` identify documents in this project; they are not release versions. Until the project becomes an actual IETF submission, it does not use Internet-Draft revision suffixes such as `-00` or `-01`.

Changes accumulate under `Unreleased` in `CHANGELOG.md`. When a release is created, its entries should be moved under a dated version heading and the corresponding Git tag and GitHub Release should be created from `main`.

## Translations

The source language for standards-track documents is expected to be English.

Translations are welcome and should be placed under:

```text
translations/<language-code>/
```

For Turkish:

```text
translations/tr/
```

Translation files should preserve the original document identifier.

Example:

```text
translations/tr/rfc-0000-problem-statement.tr.md
```

## Code of conduct

All participation is expected to follow [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md).
