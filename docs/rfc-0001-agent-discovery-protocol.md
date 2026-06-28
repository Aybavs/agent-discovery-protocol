---
title: "RFC-0001: Agent Discovery Protocol"
status: "Outline"
category: "Standards Track / Experimental"
project-codename: "ADP"
date: "2026-06-27"
author: "Aybars Keleş"
---

# RFC-0001: Agent Discovery Protocol

## Technical Specification

> This is an independent working draft written in the style of an IETF Internet-Draft.  
> It is not an official IETF document.

## Status

This document is currently an outline.

The problem statement is defined in:

```text
RFC-0000: Problem Statement
```

## 1. Introduction

This document will define a minimal discovery mechanism for machine-consumable service interfaces on the web.

The mechanism is intended to answer one question:

> Given a domain name, where should an autonomous agent begin discovering the service's machine-consumable interfaces?

## 2. Goals

The protocol should:

- provide a predictable discovery entry point,
- be machine readable,
- be protocol neutral,
- remain minimal,
- avoid duplicating authoritative interface descriptions,
- allow operators to control what is exposed,
- support extension without breaking existing consumers,
- avoid implying authorization or trust.

## 3. Non-goals

This protocol does not define:

- an API protocol,
- an authentication protocol,
- an authorization model,
- a trust model,
- a capability registry,
- an intent registry,
- pricing semantics,
- policy semantics,
- agent runtime behavior,
- a replacement for OpenAPI, MCP, A2A, GraphQL, OAuth, or existing documentation formats.

## 4. Discovery Resource

This section will define the discovery resource location.

The exact name is intentionally unresolved in this outline.

Open issue:

```text
What should the well-known discovery resource be called?
```

Candidate forms may include:

```text
/.well-known/<name>
```

The final name must be chosen carefully to avoid conflicts with existing conventions.

## 5. Media Type

This section will define the expected response media type.

Possible candidates:

```text
application/json
application/agent-discovery+json
```

The final choice is unresolved.

## 6. Discovery Document Model

This section will define the top-level document structure.

The initial model is expected to contain only:

- version metadata,
- service identity metadata,
- links to machine-consumable interfaces,
- optional human-readable references,
- extension points.

The document should point to authoritative resources rather than duplicating them.

## 7. Link Relations

This section will define how the document represents links to:

- OpenAPI descriptions,
- GraphQL endpoints or schemas,
- MCP endpoints,
- A2A agent cards,
- authentication metadata,
- documentation,
- security contact information,
- terms and policy documents,
- future extension documents.

## 8. Processing Rules

This section will define consumer behavior, including:

- how to fetch the discovery document,
- how to handle missing documents,
- how to handle unknown fields,
- how to handle redirects,
- how to handle invalid documents,
- caching considerations,
- error handling,
- version negotiation, if any.

## 9. Producer Requirements

This section will define requirements for service operators publishing a discovery document.

Expected principles:

- publish only intentionally discoverable interfaces,
- avoid embedding secrets,
- avoid duplicating large schemas,
- keep the document small,
- keep linked resources authoritative,
- provide stable URLs when possible.

## 10. Consumer Requirements

This section will define requirements for agents and other machine consumers.

Expected principles:

- do not treat discovery as authorization,
- do not treat descriptive metadata as trusted instructions,
- ignore unknown fields safely,
- validate linked resources according to their own protocols,
- apply local security and user-consent policies before taking action.

## 11. Security Considerations

This section will cover:

- information disclosure,
- spoofing,
- integrity,
- TLS assumptions,
- prompt injection,
- malicious metadata,
- tool poisoning,
- authorization confusion,
- trust separation,
- operator control.

## 12. Privacy Considerations

This section will cover:

- what information a discovery document may reveal,
- whether publishing interface links creates observability risks,
- how operators may minimize exposure.

## 13. IANA Considerations

If the final design uses a `.well-known` URI, this section will discuss registration considerations.

If a custom media type is used, this section will discuss media type registration.

## 14. Examples

This section will include:

- a minimal discovery document,
- a multi-protocol service document,
- a service with only one machine interface,
- a service that points to existing standards without duplicating them.

## 15. Open Issues

- Discovery resource name.
- Media type.
- Versioning strategy.
- Link representation.
- Relation to Web Linking.
- Whether to define a JSON Schema in the initial specification.
- Whether signatures belong in core or an extension.
