# Manifesto

## Toward Predictable Discovery for Autonomous Agents on the Web

The web has always evolved by adding small conventions that allow new classes of consumers to participate more safely and predictably.

Autonomous agents are becoming a new class of web consumer.

They do not only read pages. They may interact with services, call tools, submit requests, retrieve structured data, and act on behalf of people or organizations.

But before an agent can use a service, it must first answer a basic question:

> What machine-consumable interfaces does this service expose, and where are they?

Today, this question often requires guessing, searching documentation, parsing human-oriented pages, or relying on service-specific integrations.

This project starts from the belief that this bootstrapping problem deserves a small, open, vendor-neutral convention.

## What this project is

This project is an attempt to define a minimal discovery layer for machine-consumable service interfaces on the web.

It is intended to be:

- small,
- predictable,
- protocol neutral,
- vendor neutral,
- operator controlled,
- machine readable,
- human understandable,
- compatible with existing standards.

## What this project is not

This project is not:

- a new API standard,
- a new AI platform,
- a new agent runtime,
- a replacement for OpenAPI,
- a replacement for MCP,
- a replacement for A2A,
- a replacement for OAuth,
- a capability registry,
- an intent registry,
- a trust framework.

The goal is not to replace existing protocols.

The goal is to help agents find them.

## Core idea

A service should have a predictable way to say:

> These are the machine-consumable interfaces I intentionally expose. Here is where you can find their authoritative descriptions.

That is all.

The discovery layer should not duplicate schemas, policies, capabilities, or tool definitions.

It should point to them.

## Long-term vision

If this work succeeds, adding an agent-facing discovery document should become as ordinary as adding other small web-facing discovery resources.

A service operator should be able to publish a minimal discovery surface without adopting a specific AI vendor, agent runtime, or protocol stack.

An agent should be able to begin from a domain name and discover the machine interfaces the service has chosen to expose.

The web does not need another monolithic AI framework.

It needs a small, predictable starting point.
