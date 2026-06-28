# Agent Discovery Protocol

**Project status:** Independent working draft  
**Project codename:** ADP  
**Current focus:** Problem statement and discovery requirements

Agent Discovery Protocol is an early, vendor-neutral proposal for discovering machine-consumable service interfaces on the web.

The project starts from a narrow question:

> When an autonomous agent encounters a web service for the first time, how should it discover which machine interfaces the service exposes and where those interfaces are located?

This repository does not define a new API protocol, authentication model, capability model, agent runtime, or trust framework.

It focuses on the discovery problem.

## Why this exists

Many web services expose machine-consumable interfaces such as REST APIs, OpenAPI descriptions, GraphQL schemas, MCP endpoints, agent identity documents, documentation, authentication metadata, or other machine-facing resources.

However, when an autonomous agent only knows a domain name, there is no general, vendor-neutral, protocol-neutral starting point that tells the agent where those interfaces are located.

This project explores that bootstrapping problem.

## Documents

| Document | Status | Description |
|---|---:|---|
| [`RFC-0000 — Problem Statement`](docs/rfc-0000-problem-statement.md) | Working draft / English | Explains the discovery gap without proposing a solution. |
| [`RFC-0000 — Problem Statement (TR)`](translations/tr/rfc-0000-problem-statement.tr.md) | Translation | Turkish working translation of the problem statement. |
| [`RFC-0001 — Agent Discovery Protocol`](docs/rfc-0001-agent-discovery-protocol.md) | Planned outline | Planned technical specification. |
| [`RFC-0002 — Rationale and Design Decisions`](docs/rfc-0002-rationale-and-design-decisions.md) | Planned outline | Planned design rationale. |
| [`Manifesto`](docs/manifesto.md) | Planned outline | Vision and long-term direction. |

The English `RFC-0000` is the **canonical** version of the problem statement. The Turkish document is a translation of it.

## Current status

This project is not an official IETF document.

The `RFC-0000`, `RFC-0001`, and `RFC-0002` labels are internal project identifiers, not RFC Editor numbers.

The current goal is to develop the idea in the open, gather feedback, and refine the problem statement before proposing a concrete specification.

## Design principles

- Discovery first
- Protocol neutral
- Minimal core
- Machine readable
- Human understandable
- Vendor neutral
- Backward compatible
- Extensible
- Operator controlled disclosure
- Separation of discovery from authorization

## Scope

This project is about discovering where machine interfaces are located.

It does not attempt to replace:

- OpenAPI
- GraphQL
- MCP
- A2A
- OAuth
- existing API documentation formats

Instead, it aims to define a small discovery layer that can point to them.

## Repository structure

```text
agent-discovery-protocol/
├── README.md
├── LICENSE.md
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── SECURITY.md
├── CHANGELOG.md
├── docs/
│   ├── rfc-0000-problem-statement.md
│   ├── rfc-0001-agent-discovery-protocol.md
│   ├── rfc-0002-rationale-and-design-decisions.md
│   └── manifesto.md
├── translations/
│   └── tr/
│       └── rfc-0000-problem-statement.tr.md
├── examples/
│   ├── README.md
│   ├── minimal-agent-discovery.json
│   └── multi-protocol-service.json
└── schema/
    └── agent-discovery.schema.json
```

The files under `schema/` and `examples/` are **non-normative placeholders** and do not define the protocol. The discovery document format is intentionally not specified until `RFC-0001`.

## Contributing

Feedback is welcome.

The most useful feedback at this stage is about:

- whether the problem is accurately described,
- whether existing mechanisms already address part of the problem,
- whether the proposed scope is too broad or too narrow,
- whether the terminology is clear,
- whether the security considerations are complete,
- and what requirements a minimal discovery mechanism should satisfy.

Please read [`CONTRIBUTING.md`](CONTRIBUTING.md) before opening a large proposal.

## License

This repository uses a dual-license model:

- Documentation is licensed under Creative Commons Attribution 4.0 International.
- Code, schemas, and examples are licensed under Apache License 2.0.

See [`LICENSE.md`](LICENSE.md).
