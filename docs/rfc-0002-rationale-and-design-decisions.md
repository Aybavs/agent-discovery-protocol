---
title: "RFC-0002: Rationale and Design Decisions"
status: "Outline"
category: "Informational"
project-codename: "ADP"
date: "2026-06-27"
author: "Aybars Keleş"
---

# RFC-0002: Rationale and Design Decisions

> This is an independent working draft written in the style of an IETF Internet-Draft.  
> It is not an official IETF document.

## Status

This document is currently an outline.

It will explain why the Agent Discovery Protocol is designed the way it is.

## 1. Introduction

This document records the reasoning behind the design decisions made in RFC-0001.

Its purpose is to separate the protocol definition from the reasoning behind the protocol.

## 2. Why a discovery layer?

This section will explain why the project focuses on service-interface discovery rather than communication, capability modeling, trust, pricing, or policy semantics.

## 3. Why not define a new API protocol?

This section will explain why the protocol should point to existing machine interfaces rather than replace them.

## 4. Why protocol neutrality?

This section will explain why the discovery layer should be able to reference multiple interface types such as OpenAPI, GraphQL, MCP, A2A, and future protocols.

## 5. Why minimal core?

This section will explain why the initial specification should remain small and avoid defining capabilities, intents, pricing, policy, or trust.

## 6. Why indirection instead of duplication?

This section will explain why the discovery document should link to authoritative descriptions instead of copying their content.

## 7. Why operator control?

This section will explain why services must explicitly control what they make discoverable.

## 8. Relationship to OpenAPI

This section will explain how ADP relates to OpenAPI and why it is not a replacement.

## 9. Relationship to MCP

This section will explain how ADP relates to MCP and why discovery and communication are separate concerns.

## 10. Relationship to A2A

This section will explain how ADP relates to agent-to-agent identity and collaboration mechanisms.

## 11. Relationship to llms.txt

This section will explain how ADP differs from LLM-oriented documentation hints.

## 12. Why not define capability or intent semantics in v0.1?

This section will explain why capability and intent modeling should be separate future work.

## 13. Security rationale

This section will explain the design choices around:

- authorization separation,
- information disclosure,
- prompt injection,
- malicious metadata,
- future signatures,
- trust extensions.

## 14. Naming rationale

This section will record endpoint and project naming decisions once they are made.

## 15. Future extensions

This section will explain which areas are intentionally deferred:

- capability metadata,
- policy documents,
- trust metadata,
- pricing metadata,
- event discovery,
- streaming discovery,
- signatures,
- federation.
