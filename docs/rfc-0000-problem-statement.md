---
title: "RFC-0000: Problem Statement"
status: "Working Draft"
category: "Informational"
project-codename: "ADP"
lang: "en"
canonical: true
date: "2026-06-27"
author: "Aybars Mete Keleş"
---

# RFC-0000: Problem Statement
## Service Interface Discovery for Autonomous Agents on the Web

---

## Status of This Memo

This document is **not** an IETF document. It is not published by the IETF, the IRTF, the RFC Editor, or any other standards body. It is an **independent working draft**, published for open discussion, that adopts the writing conventions and rigor of an IETF Internet-Draft.

The label "RFC-0000" assigned to this document is **not** a number issued by the RFC Editor. It is an **internal project identifier** used to number the related set of documents consistently. Likewise, "ADP" is **not** a final name; it is a **project codename**. Naming is deliberately deferred and is among the last decisions to be made, after the problem and the technical solution have matured.

This document proposes no solution. Its sole purpose is to make a specific, currently unstandardized problem on the web precise, and to lead the reader to conclude, through their own reasoning, that a real problem exists here for which no common mechanism is yet available. The proposed solution to this problem is defined in a separate specification document, RFC-0001.

Feedback and discussion are welcome and encouraged.

---

## Abstract

For more than three decades, the web has evolved by adapting to the classes of client that consume it. As the needs of different machine consumers emerged, the web developed small and predictable discovery conventions for specific problems: how a crawler should traverse a site, how an identity client should learn a provider's configuration, to whom a security researcher should report a vulnerability. Each of these questions was answered by a small, shared convention layered onto the web.

Today a new class of consumer has appeared: **autonomous agents** that carry out tasks on behalf of a human, in real time. These clients do not merely read content; they interact with services, initiate operations, and must work with services they have never integrated with before. Yet for this class of consumer, the web does not yet have a common discovery convention.

This document defines that gap. Before proposing any new solution, it states precisely the problem that must be solved: when an autonomous client encounters a service it has not previously integrated with, there is no standard way for it to determine which machine-consumable interfaces that service exposes, or where those interfaces are located. The document examines this problem in light of the web's history of discovery; shows, in neutral terms, that each existing mechanism solves a **different** problem; grounds the problem in concrete use cases; and enumerates the properties any solution must have. The solution itself is out of scope for this document.

---

## 1. Introduction

For its entire existence, the web has never been a static system serving a single kind of user. On the contrary, the history of the web is a history of continual adaptation to changes in the nature of the clients that consume it.

This adaptation has usually been achieved not by designing large, ambitious systems, but by agreeing on small, shared conventions. How a search-engine crawler should traverse a site, where an identity client should learn a provider's configuration, to whom a security researcher should report a vulnerability — each of these has been solved with a small, predictable, machine-readable discovery convention layered onto the web. What these conventions have in common is that they let a machine reach the basic information it needs about a system **without guessing, in a standard way**.

This document argues that the web's newest class of consumer — autonomous agents — currently lacks the kind of discovery convention that some of the earlier client classes possess. As a result, when an agent encounters a new service, it is forced to re-solve a problem the web has already solved for earlier classes — and this time service by service, with brittle methods.

The purpose of this document is not to provide a solution. Its purpose is to show that this problem is real, concrete, and unstandardized. No mechanism, format, or technical design will be proposed anywhere in this document. What is asked of the reader is only that, by the end, they see the problem clearly and reach the judgment that a common problem exists here that ought to be solved. The proposed technical solution to this problem is the subject of RFC-0001.

### 1.1. Scope of This Document

This document addresses only the **discovery** problem. This document does not:

- define an interface format,
- define a communication protocol,
- define an authentication or authorization model,
- define a capability or intent model,
- define a trust framework.

This document examines only a single question, and shows that this question has no standard answer today: **"When a machine consumer encounters a service it has never seen before, where should it begin to find that service's machine-consumable interfaces?"**

### 1.2. Intended Audience

This document is written to address two audiences at once. The first is technical readers experienced in web standards, protocol design, and distributed systems. The second is readers new to the subject who nonetheless wish to understand the nature and importance of the problem. The document aims to use terminology rigorously while explaining each core concept from first principles.

---

## 2. The Evolution of Machine Consumers on the Web

The purpose of this section is to show that the problem at hand is not an exceptional situation arising from a new technology, but the next step in the natural evolution of the web. To do so, we trace the development over time of the classes of client that consume the web.

### 2.1. First Class: The Human Reader

The web was first designed for humans. Documents were written in a markup language formatted for human reading; browsers were developed to present those documents to the human eye. In this period the web's primary consumer was a human who read the screen, followed links, and made decisions by their own reasoning.

For this class, "discovery" was a cognitive act performed by a human. A person would look at a page, grasp its meaning, and click the relevant link. No special discovery information needed to be provided to a machine, because the consumer was a human who could infer meaning.

### 2.2. Second Class: The Crawler and Indexer

As the web grew, the need arose to traverse and index content at scale. Search engines built machines that automatically roamed the web — crawlers. This was the web's first large class of **machine consumer**.

A crawler differs from a human: it does not grasp meaning as a human does, nor interpret content as a human does. It merely traverses and reads at scale. This new class of client created a need that had not existed before: a crawler needed to know, **predictably**, how it should traverse a site, which sections it should not enter, and what content existed.

The web answered this need not by designing a large system, but with small, shared conventions. A plain-text file at the root of a site declared access rules to crawlers; another convention provided a machine-readable list of the site's content. These were small, predictable, and publicly available conventions. This is the clearest example of the web meeting a machine-consumer class's discovery need with a shared convention.

### 2.3. Third Class: The Mobile Application Era

In the following period, a new kind of client that consumed the services behind the web became widespread: mobile applications and rich client applications. These applications presented an interface to the user while talking to services programmatically in the background.

However, interaction in this period rested largely on **point-to-point**, **pre-built** integrations. Each application knew the service it would talk to at development time; developers inspected that service's interface by hand; the integration was written once, embedded in code. **No general discovery convention emerged** in this era, because the client was the product of a developer who already knew, in advance, which service to talk to and how. Even so, this period began an important transition: the web was becoming an infrastructure that served not only documents to humans but data and operations to machines.

### 2.4. Fourth Class: The Programmatic API Client

As programmatic consumption matured, machine-to-machine interaction became an explicit discipline. Services began publishing structured, machine-readable descriptions of the interfaces they offered. These descriptions described which operations an interface provided, which parameters it expected, and which responses it returned.

This was a significant advance for machine consumers. But discovery here still happened largely **through a human**. The typical flow was: a developer learns somehow that a service exists; finds that service's documentation as a human; reads the interface description; and writes the integration **once, at design time**. Although the description itself was machine-readable, the answer to "which interfaces does this service have, and where do I begin?" was usually a piece of knowledge that a human found and carried into code.

### 2.5. Fifth Class: The Autonomous Agent (Today)

The new class of consumer the web faces today differs qualitatively from all the previous classes.

An autonomous agent is a machine client that acts on behalf of a human, but whose integration was not wired by hand by a developer at design time. A user asks the agent to carry out a task; to complete that task, the agent may encounter, **at run time**, services it has never integrated with, and may be required to understand and interact with them. This departs from the previous classes in critical ways:

- **Unlike a crawler**, the agent does not merely read; it can initiate operations and interact.
- **Unlike a mobile application**, the service the agent will encounter may not be known in advance; the integration is not embedded in code.
- **Unlike an API client**, the decision to discover and integrate is made not by a developer at design time, but by the agent itself at run time.

This is the new situation in the web's evolution: the consumer is no longer a developer who writes an integration once, but a client that encounters services it has never seen before, in real time and autonomously.

### 2.6. The Observation Drawn from This Evolution

The observation drawn from this evolution is **not** that a discovery convention necessarily emerged for every consumer class. For some classes — particularly the crawler class — specific and predictable conventions developed; in the mobile era, discovery was largely solved point-to-point and no general convention emerged. The real observation is this: when a class of machine consumer has produced a clear and widespread discovery need, the web has tended, over time, to meet that need with small, shared conventions.

The autonomous agent class, however, has produced such a widespread discovery need today and yet lacks a shared convention to meet it. The remainder of this document examines precisely what this absence means, why it constitutes a problem, and why existing mechanisms do not solve it.

> **Section takeaway.** As machine-consumer classes have produced clear discovery needs, the web has tended to develop small and predictable conventions for specific problems. The autonomous agent class produces such a need today, but no shared convention yet meets it.

---

## 3. Terminology

This section defines the core terms used throughout the document.

The key words "MUST", "MUST NOT", "SHOULD", "SHOULD NOT", and "MAY" are to be interpreted as described in RFC 2119 and RFC 8174, and only when they appear in this uppercase form. Because this document is not a specification, normative key words appear only in Section 8, which discusses the properties any solution must have, in order to indicate the strength of requirements.

**Service:** A web system reachable over HTTP, published under a domain. A service may present a human-facing website, a programmatic interface, or both.

**Machine consumer:** Any program that consumes the web automatically, without a human's cognitive reasoning. Crawlers, programmatic API clients, and autonomous agents fall into this class.

**Autonomous agent:** A machine consumer that carries out tasks on behalf of a human and that, to complete those tasks, may encounter and interact with services whose integration was not wired by hand at design time.

**Machine interface:** Any access point or capability a service exposes to be consumed programmatically by machine consumers. A service may expose zero, one, or several machine interfaces; these interfaces may rest on different protocols.

**Discovery:** The process by which a machine consumer reaches the basic information it needs about a service — in particular, which machine interfaces the service exposes and where they are located — without prior special integration.

**Cold encounter:** The situation in which a machine consumer meets, for the first time, a service it has never integrated with, knowing only that service's domain. The problem addressed in this document concerns this situation directly.

**Interface description:** A document that describes, in machine-readable form, the structure, operations, and behavior of a machine interface. Interface descriptions are **not the subject** of the discovery problem addressed here; they are what is discovered — that is, the content reached after discovery has taken place.

---

## 4. Problem Statement

This section defines the problem at the center of the document as precisely as possible.

### 4.1. Statement of the Problem

When an autonomous agent encounters a service it has never integrated with in order to carry out a task — that is, at the moment of a **cold encounter** — there is **no standard, predictable method** by which it can determine which machine interfaces that service exposes and where those interfaces are located.

The essence of the problem is carried by a single sentence:

> *An agent knows only a domain. There is no prior integration. Where does it begin?*

When this question has no standard answer, the agent is forced to fall back on a set of heuristic, brittle, service-specific strategies: trying to parse and interpret pages formatted for humans; guessing common paths where an interface might be found; trying to find documentation via search; or requiring a human developer to build a bespoke integration for that service before the agent runs.

### 4.2. The Two Core Components of the Problem

The problem reduces to two distinct questions, neither of which has a standard answer today:

1. **The existence question:** "Does this service expose machine-consumable interfaces?" An agent, looking only at a domain, cannot know predictably whether that service can be consumed programmatically.

2. **The location question:** "If it does, where are those interfaces?" Even if a service does expose interfaces, the agent cannot determine in a standard way where they are located, which protocols they rest on, or where to reach the relevant descriptions.

### 4.3. The Bootstrapping Nature of the Problem

At its core the problem is one of **bootstrapping**. Most existing tools and standards assume that discovery **has already taken place**. An interface description is useful when the agent already knows that interface's existence and location; a communication protocol is useful when the agent already knows where the relevant server is. None of them makes the very first question — where to begin given only a domain — its own subject.

### 4.4. The "Unstandardized" Dimension of the Problem

The critical point to emphasize is not that the problem is technically **unsolvable**. On the contrary, every agent developer already solves this problem by their own method, with their own service-specific solutions. The problem is that these solutions are **not common and not predictable**. Every consumer writing a separate integration for every service is a cost that existed in earlier periods of the web as well, but was overcome with shared conventions; for the agent class, this cost is now being paid again.

> **Section takeaway.** The problem is one of bootstrapping: given only a domain, there is no common, predictable answer to where a machine consumer should begin to find a service's interfaces. The problem is not unsolvable; it is unstandardized.

---

## 5. Current Discovery Landscape

This section examines the discovery and description mechanisms that exist on the web today for machine consumers. An important principle governs this examination: **no mechanism is criticized, and none is described as "insufficient."** Each of these mechanisms successfully solves the problem it was designed for. The purpose of this section is to set out, in neutral terms, **which** problem each one solves and what its scope is. Each mechanism is treated with the same common frame: its purpose, the problem it solves, and its scope.

### 5.1. Crawler Access Rules (Robots Exclusion)

**Purpose:** To let a site's operator tell automated crawlers which sections they may or may not traverse.

**Problem it solves:** Management of crawler access. It offers a shared convention indicating which parts of a site it is appropriate for a crawler to reach.

**Scope:** **Permission and exclusion** regarding the traversal of content by crawlers. This mechanism does not aim to describe a service's machine interfaces or report their location; by design it solves an entirely different problem.

### 5.2. Content Enumeration (Sitemaps)

**Purpose:** To provide indexers with a machine-readable list of the content addresses on a site.

**Problem it solves:** Discoverability of content. It lets indexers learn a site's content addresses completely and efficiently.

**Scope:** **Enumeration of content addresses** for the purpose of indexing. This mechanism says where content is; it does not aim to report the existence or location of a service's programmatic interfaces. That is a different problem.

### 5.3. Identity Provider Configuration Discovery (OpenID Connect Discovery)

**Purpose:** To let an identity client learn the configuration information of an identity provider.

**Problem it solves:** Discovery of the configuration needed to initiate an authentication flow. It lets the client learn the provider's relevant addresses and parameters.

**Scope:** **Configuration discovery** specific to a particular identity protocol. This mechanism is highly effective within its own domain; but it is specific to that protocol and does not aim at general service-interface discovery. It therefore solves a different problem.

### 5.4. Security Contact Information (security.txt)

**Purpose:** To let a security researcher learn to whom they should report a vulnerability found in a service.

**Problem it solves:** Easing the vulnerability-disclosure process. It offers a shared convention for reaching a service's security contact information.

**Scope:** **Security contact.** This mechanism does not aim to describe or discover a service's machine interfaces; it solves an entirely different problem. It is mentioned here because it is a successful example of the web's tradition of solving problems with small, shared discovery conventions.

### 5.5. Interface Descriptions (OpenAPI and Similar)

**Purpose:** To describe, in machine-readable form, the structure of a particular HTTP interface — its operations, parameters, and responses.

**Problem it solves:** The **description** of an interface and the understanding of that interface's capabilities. An interface description carries a discovery dimension of its own: a programmatic client can read such a description and understand how to interact with the interface.

**Scope:** The distinction here is subtle and requires care. An interface description makes an interface strongly understandable **once that interface has been found**. However, it does not aim to answer, from a standard starting point at the domain level, **how many** such descriptions exist under a given domain, **where** they are published, or whether the service **also exposes other protocols**. A service may expose no description, a single description, or several descriptions belonging to different protocols. In other words, a description answers "how do I use this interface?"; it does not aim to answer "which interfaces does this service have, and where do I begin?" at the domain level.

### 5.6. Agent–Service Communication Protocols (Model Context Protocol)

**Purpose:** To define the interaction between an agent or client and a service — how the client uses the tools and data sources the service exposes.

**Problem it solves:** **Communication** between client and service. It lets a client use a service's capabilities through a standard protocol.

**Scope:** This mechanism defines the interaction between a client and a server. However, gathering which such interfaces a web service exposes — and, where present, alongside which other interfaces — into a general service-discovery index, starting only from the domain level, is not the direct scope of this protocol. The protocol defines **how** communication proceeds; it does not aim at this indexing-and-bootstrapping question. For communication to begin, the location of the relevant server must be known; how that location is to be found from the domain alone is a separate problem.

### 5.7. Agent Identity and Collaboration Approaches (Agent-to-Agent)

**Purpose:** To describe, in machine-readable form, an agent's identity, capabilities, and how to communicate with it, to other agents; and to enable agents to discover one another and collaborate.

**Problem it solves:** Agents recognizing, discovering, and collaborating with one another. These approaches **define a discovery mechanism of their own**: an agent publishes its machine-readable identity and capability description at a predictable, conventional location, and other agents find it there. They therefore provide effective discovery in the agent-to-agent context.

**Scope:** These approaches generally focus on modeling the discovered entity around **agent identity**. The problem addressed in this document, however, sits in a broader context: to find, in a single service-interface discovery context and starting only from a domain, the various kinds of machine interface that any web service — an e-commerce site, a reservation service, a public-sector service — chooses to make discoverable. For this reason agent-to-agent approaches do not conflict with this problem space; but they are not within the same scope as the general service-interface discovery addressed in this document.

### 5.8. Documentation Hints for LLMs (llms.txt and Similar Conventions)

**Purpose:** For a site to provide, for language-model-based clients, a curated summary — readable by both humans and machines — pointing to its most important content.

**Problem it solves:** Presenting content to language models in a simplified, curated form. It lets a client reach a list pointing to a site's most valuable documentation and content pages.

**Scope:** This is **not a formal IETF or comparable standard**, but a community convention. Its scope is **content curation** for language models; it does not aim to report the existence and location of a service's programmatic machine interfaces in a service-interface discovery context. It points to content, not to interfaces. This too is a different problem from the one defined in this document.

### 5.9. Summary of the Landscape (A Neutral Comparison)

The following table summarizes the examined mechanisms in neutral terms. Nowhere in the table is the word "insufficient" used; instead, it is shown that the problem each mechanism solves is **different**. The final column indicates whether the mechanism addresses the cold-encounter service-interface discovery problem defined in this document.

| Mechanism | Primary Consumer | Problem It Solves | Addresses Cold-Encounter Service-Interface Discovery? |
|---|---|---|---|
| Crawler access rules | Crawler | Management of crawler access | No — different problem |
| Content enumeration | Indexer | Enumeration of content addresses | No — different problem |
| Identity provider discovery | Identity client | Configuration discovery for a particular protocol | No — different problem |
| Security contact information | Security researcher | Security contact | No — different problem |
| Documentation hints for LLMs | Language-model client | Content curation | No — points to content, not interfaces |
| Interface descriptions | Programmatic client | Description of an interface | Partly — after an interface is found; does not aim at a domain-level index |
| Agent–service communication protocols | Agent / client | Client–service communication | Partly — defines communication; does not aim at a general service index |
| Agent identity / collaboration approaches | Agent | Agent identity and collaboration | Partly — models the entity around agent identity; not a general service-interface index |

The pattern this table reveals is that each mechanism either solves a **different problem**, or — even where it provides effective discovery within its own domain — that discovery is not a general service-interface index. This is not a flaw; these mechanisms were not designed for it. The picture that emerges is simply that no mechanism has yet taken this specific problem into its own scope.

> **Section takeaway.** Existing mechanisms either enumerate content, describe a known interface, enable known endpoints to communicate, or make an agent's identity discoverable in an agent-to-agent context. None defines, for any web service, a general cold-start service-interface discovery layer that begins from the domain alone.

---

## 6. Gap Analysis

The previous section examined each existing mechanism on its own. This section names the resulting gap directly and shows why it is not closed by a natural extension of the existing mechanisms.

### 6.1. The Precise Definition of the Gap

The gap lies between two classes of mechanism. On one side are discovery conventions oriented toward **content**; these address the traversal and enumeration of a site's content, but content is not the same thing as a service's **programmatic interfaces**. On the other side are description, communication, and identity mechanisms oriented toward **the interface and the agent**; these address how an interface is described, how a client and a service communicate, or how an agent's identity is expressed. This second group, even where it provides effective discovery within its own context, is either **specific to the context** of the relevant interface or agent, or does not aim to gather a service's **heterogeneous interfaces into a single index**.

The gap lies exactly between these two: there is no shared starting point that would let a machine consumer learn the existence and location of a service's machine interfaces **without traversing content** and **without assuming in advance that a particular protocol or agent model exists**, starting only from a domain.

### 6.2. Answers to "Why Doesn't an Existing Mechanism Solve This?"

Addressing one by one the objections an experienced reader will rightly raise is the most honest way to test the reality of the problem.

**"Isn't an interface description (OpenAPI) already a discovery method?"**
An interface description describes an interface, and that description carries a discovery dimension of its own. But this holds **once an interface has already been found**. The description does not answer, from a standard starting point at the domain level, how many descriptions exist under a given domain, where they are published, or whether the service also exposes other protocols. In other words, it strongly answers "how do I use this?"; it does not answer "where do I begin?" at the domain level.

**"Doesn't an agent–service communication protocol (MCP) close this gap?"**
A communication protocol defines the interaction between a client and a server. But gathering which such interfaces a web service exposes — and, where present, alongside which other interfaces — into an index starting from the domain level is not the direct scope of the protocol. Moreover, for communication to begin, the location of the relevant server must already be known; how that location is to be found from the domain alone is not a question the protocol targets.

**"Don't agent identity and collaboration approaches (A2A) do this job?"**
These approaches define a real and effective discovery in the agent-to-agent context; the relevant identity description is published at a predictable, conventional location. The objection therefore cannot be built on "the location is assumed to be known." The distinction sits on a different axis: these approaches generally model the discovered entity around agent identity and focus on a single agent. Gathering the various kinds of machine interface a service chooses to make discoverable into a single general index is a different scope. These approaches are a strong agent-discovery layer; they are not a general service-interface discovery layer.

**"A service can put all its links on its home page; can't the agent read them?"**
An agent can try to parse a page formatted for humans. But this is exactly the approach the web has already rejected for the crawler class: forcing a machine consumer to interpret human-readable presentation is brittle, unpredictable, and requires re-engineering for every service. The web developed shared conventions for crawlers precisely for this reason; accepting the same brittleness for the agent class would disregard a lesson already learned.

### 6.3. The Unifying Statement of the Gap

The common answer to all these objections fits in a single sentence: each existing mechanism either solves a **different problem**, provides a discovery **specific to a particular context**, or does not aim to gather a service's **heterogeneous interfaces into a single general index**. None makes the question — given only a domain, where a machine consumer should begin, for any web service — its own subject. The gap is real, and it can be closed only by a mechanism that explicitly makes this bootstrapping question its own subject.

> **Section takeaway.** The gap lies between content discovery and interface description/communication/agent identity. Existing mechanisms may provide effective discovery within their own contexts; but none makes it its own subject to gather any web service's heterogeneous interfaces into a single index that begins from the domain alone.

---

## 7. Use Cases

This section offers scenarios that make the defined problem concrete. None of the scenarios proposes a solution; each shows how, today, the situation requires brittle, service-specific effort.

### 7.1. An Agent Acting on a User's Behalf

A user asks a personal agent to arrange travel for them. The agent encounters the domain of an airline it has never integrated with. What it needs to know is simple: does this airline expose a machine-consumable interface, and if so, where? Today the agent cannot answer this question in a standard way; it must rely on a bespoke integration pre-built for this airline, try to parse human-readable pages, or guess common paths. For each airline, this effort is paid again.

### 7.2. An Enterprise Agent Evaluating a New Vendor

An agent supporting a company's procurement process is evaluating the site of a new software vendor. The agent needs to find the vendor's programmatic interfaces and the relevant terms. Today this requires vendor-specific research, because the agent cannot know predictably whether the vendor's interfaces exist and where they are located. This is a recurring, unstandardized cost at scale.

### 7.3. A Developer's Agent Pointed at a Third-Party Service

A developer's coding agent is tasked with producing integration code for a third-party service. The agent is expected to find that service's interface description — without the developer handing over the relevant address by hand. Today the developer must usually supply the address of the relevant description to the agent by hand, because the agent cannot determine, starting only from the domain, whether the service's description exists and where it is located.

### 7.4. A Service Exposing Only a Single Protocol

A service exposes only a single kind of machine interface; it may not expose a conventional HTTP interface at all. An agent must nonetheless find the existence and location of that single interface. This scenario shows why discovery should not depend on a particular protocol: if discovery assumes only one kind of protocol, services exposing a different protocol remain invisible.

### 7.5. A Service Exposing Several Protocols

A service exposes several kinds of machine interface at once: a conventional HTTP interface, a query interface, an agent communication interface, and an agent identity description. But an agent, looking only at the domain, cannot know that all of these exist. This scenario shows that the problem is not limited to the "are there no interfaces at all?" case: even when interfaces are **abundant**, the agent cannot learn their list and locations in a standard way; it may discover some and miss others.

> **Section takeaway.** In every scenario the agent's need is simple — "which machine interfaces does this service have, and where?" — yet there is no standard way to reach this simple information. The result is pre-built bespoke integrations, human intervention, or brittle guessing.

---

## 8. Requirements for a Discovery Mechanism

This section enumerates the properties that **any** mechanism solving the problem defined above must have. A critical distinction applies here: this section **does not define the solution.** It only sets out the requirements a reasonable solution must satisfy. The form, structure, and mechanics of the solution are the subject of RFC-0001.

This section expresses **candidate requirements** for RFC-0001; the normative language used here does not imply that this document defines a protocol. The uppercase key words in this section are used with their RFC 2119 and RFC 8174 meanings.

### 8.1. Predictability

The mechanism MUST be locatable knowing only a domain, without prior integration or out-of-band knowledge. The entire point of discovery is to eliminate guessing.

### 8.2. Machine-Readability

The mechanism MUST be in a form a program can consume without having to interpret human-readable presentation. The lesson the web learned for the crawler class applies directly here.

### 8.3. Protocol Neutrality

The mechanism MUST NOT privilege or assume any single interface protocol. A service may use a single protocol, several protocols, or none; the mechanism MUST be able to accommodate all of these cases.

### 8.4. Minimalism

The mechanism SHOULD be small enough to be produced trivially and consumed trivially. The discovery layer SHOULD NOT become a heavy data model. Successful conventions start small and stay small.

### 8.5. Indirection, Not Duplication

The mechanism SHOULD point to **where** authoritative descriptions are located; it should not re-encode the content of those descriptions. This both keeps the layer small and preserves the single-source-of-truth principle. This principle is the central one that protects a future solution from unnecessary growth.

### 8.6. Operator Control

The operator of a service MUST be able to control explicitly which interfaces are made discoverable. Discoverability MUST depend on the operator's deliberate decision; a mechanism MUST NOT be used without granting the operator full control over what is exposed. This requirement is the direct counterpart of the information-disclosure consideration addressed in Section 11.2.

### 8.7. Backward Compatibility and Extensibility

The mechanism MUST allow new needs to be added without breaking existing consumers. It MUST tolerate information it does not recognize; that is, a consumer encountering information it does not understand MUST be able to ignore it safely. This makes it possible for the ecosystem to grow over time without breaking the core.

### 8.8. Separation from Authorization

The existence of a discovery surface MUST NOT carry any implication about the access rights of the relevant resources. Discovery says that something exists and where it is located; it does not say whether one has the right to access it. Authentication and authorization MUST remain in the domain of existing standards.

### 8.9. Low Adoption Cost

The mechanism SHOULD be deployable by an ordinary service operator without requiring specialized infrastructure. The spread of a convention depends directly on how easy it is to implement.

### 8.10. The Common Spirit of the Requirements

Read together, these requirements describe a discovery layer that is small, predictable, protocol-neutral, operator-controlled, and respectful of existing standards. Note that this section still does not describe a solution; it only enumerates the properties a solution must have.

> **Section takeaway.** The solution must be small, predictable, protocol-neutral, operator-controlled, extensible, and respectful of existing standards. But these properties do not define the solution; they only draw its boundaries.

---

## 9. Non-Goals

To keep the problem singular and clear, this section states explicitly which topics fall **outside** the scope of this document and therefore of the defined discovery problem. Each of these topics is legitimate and important; but none is part of the discovery problem, and mixing them into it would needlessly enlarge and blur the problem.

The following are **not goals** of this document or of the discovery problem addressed:

- **Capability and intent semantics.** Modeling a service's capabilities or an agent's intents in a standard way is a problem independent of discovery.
- **Authentication, authorization, and trust.** How access rights to a resource are determined and how parties come to trust one another is the subject of existing and future separate standards.
- **A communication or messaging protocol.** How an agent and a service talk is a separate problem that arises after discovery has taken place, and established approaches exist for it.
- **Pricing, terms, and policy semantics.** Modeling a service's terms of use, pricing, or policies in machine-readable form is a topic separate from discovery.
- **Selection and ranking among services.** Which of the discovered services an agent chooses — ranking, evaluation, marketplace logic — is the subject of decisions that come after discovery.
- **The interface descriptions themselves.** How interfaces are described is already the domain of existing standards. Discovery points to the location of those descriptions; it does not redefine their content or format.

The explicit exclusion of these non-goals is the source of the problem's strength. When a single problem is solved cleanly, the remaining topics can be added on top of it as independent layers.

---

## 10. Relationship to Existing Standards

This section clarifies the relationship of the defined discovery problem to existing standards. The core principle here is that this problem **does not compete** with any of the existing standards; it is **orthogonal** to them and complements them.

This orthogonality can be expressed as follows:

- Interface description standards **describe an interface**.
- Agent–service communication protocols **define the communication between a client and a service**.
- Agent identity and collaboration approaches **define an agent's identity and make it discoverable in an agent-to-agent context**.
- The discovery problem defined here, by contrast, concerns only **discovering where these are located in the context of any web service**.

These topics sit on different axes. One does not replace another; one is neither above nor below another. When a discovery convention matures, it does not diminish the value of the existing standards; on the contrary, it increases their value by making them findable by an agent in a cold encounter. This document therefore makes no claim to replace any existing standard; it only shows that the question of how an agent should, from the very beginning, find the interfaces in which those standards are realized does not yet have a common answer.

---

## 11. Security Considerations

This section addresses the security dimension of the defined problem at the **problem level**. The aim is not to discuss the security properties of a particular solution — since this document proposes no solution — but only to point to the security considerations inherent in the nature of a discovery layer.

### 11.1. Discovery Does Not Mean Access

The existence of a discovery surface does not mean that the relevant interfaces are publicly accessible. Reporting that something exists and where it is located is entirely separate from granting the right to access it. Authentication and authorization remain in the domain of existing standards.

### 11.2. Information-Disclosure Consideration

A discovery surface, by its nature, makes visible which interfaces a service has. This is a matter for the service operator to consider: the operator must decide deliberately what to make discoverable. The existence of some interfaces may not be something one wishes to announce openly. This is a known consideration also encountered in existing discovery conventions, and it is expressed as a requirement in Section 8.6.

### 11.3. Integrity and Spoofing

The accuracy and integrity of the information read from a discovery surface matters for security. Incorrect or spoofed discovery information could direct an agent to the wrong interfaces. Transport-layer security (TLS) addresses a significant part of this risk; additional integrity and authenticity guarantees could be the subject of future separate documents (for example, a signature-based extension).

### 11.4. Discovery Does Not Establish Trust

A discovery surface is not expected to guarantee the authenticity or trustworthiness of the interfaces it points to. Establishing trust — verifying that an interface is genuinely served by the party it claims to be — is a problem separate from discovery and is out of scope for this document.

### 11.5. Semantic and Instruction Injection Risk

In the autonomous agent ecosystem, the security concerns a discovery surface raises are not limited to transport security, spoofing, and information disclosure. Because the information obtained during discovery is read directly by an agent and often incorporated into its planning context, it constitutes an attack surface in its own right.

In particular, when human-readable descriptions, documentation links, tool descriptions, or policy text encountered during discovery are consumed by an agent, they can become a vector for **prompt injection, tool poisoning, and malicious metadata**. An agent can be steered by a malicious service if it treats descriptive metadata read from the discovery surface as a trusted instruction.

For this reason, a fundamental principle must apply in any solution and in every agent that consumes it: **descriptive metadata must not be treated as a trusted instruction.** Descriptions and text coming from a discovery surface should be regarded not as a source that directs the agent's reasoning, but as untrusted input that must be validated and constrained. How this principle is to be applied is out of scope for this document; but the existence of this risk must be recorded explicitly for the maturity of any discovery mechanism in the agent context.

---

## 12. Future Specification Roadmap

Throughout this document, by deliberate choice, no solution has been proposed. The purpose of this section is not to describe how the problem will be solved, but to indicate **where** the solution will be defined and how this document set will take shape from here.

### 12.1. Where the Solution Lives

The proposed solution to the problem built in this document is defined in a separate specification document, RFC-0001. This separation is deliberate: the task of a problem statement is not to sell a solution but to set out the reality of the problem. The technical form of the solution can be meaningfully evaluated only after the problem is clearly understood.

### 12.2. A Layered Extension Approach

The core of the solution is intended to be kept **deliberately minimal**, in line with the requirements enumerated in Section 8 of this document. The topics noted as non-goals — capability semantics, trust and signatures, policy, pricing, event discovery, and so on — can be added on top of it as independent, separate documents rather than growing the core. In this way the discovery layer stays small while the ecosystem can grow over time. This is a direct reflection of the web's discovery tradition: start small, and add new needs as separate layers without breaking the core.

### 12.3. A Note on Naming

The name "ADP" used in this document set is a **project codename**, not a final name. Naming has been deliberately deferred. In the history of internet standards, names sometimes change years later; what is decisive is first defining the problem correctly and then making the solution technically sound. The name will be among the last decisions made once both of these conditions are met. This also means that any potential naming overlaps with existing discovery approaches are deliberately left to the design phase of the solution.

### 12.4. Closing

This document had a single goal: to lead the reader, through their own reasoning, to the conclusion that a real, currently unstandardized discovery problem exists on the web. The evolution of the web's consumer classes, the neutral examination of the current discovery landscape, the analysis of the gap, the concrete use cases, and the properties a solution must have — all of these serve to build this single conclusion.

The solution to this problem is defined in a separate specification document, RFC-0001.

---

## Appendix A. The Evolution of Machine Consumers (Summary Diagram)

The diagram below summarizes the evolution of the client classes described in Section 2 and the discovery status of each class.

```
   CONSUMER CLASS             STATE OF THE DISCOVERY NEED
   ──────────────             ───────────────────────────

   Human Reader         →     Discovery is the human's cognitive act
        │                     (no special machine convention required)
        ▼
   Crawler /            →     Met with shared conventions
   Indexer                    (crawler access, content enumeration)
        │
        ▼
   Mobile Application   →     Point-to-point, pre-built
                              (no general discovery convention emerged)
        │
        ▼
   Programmatic         →     Interface descriptions became common
   API Client                 (discovery still through a human)
        │
        ▼
   Autonomous Agent     →     WIDESPREAD NEED, NO SHARED CONVENTION
   (Today)                    (the gap defined by this document)
```

---

## Appendix B. Informative References

The following documents point to the existing standards and conventions that form the context of this work. These references are informative; because this document is not a specification, it contains no normative references.

- RFC 2119 — Key words for use in RFCs to Indicate Requirement Levels.
- RFC 8174 — Ambiguity of Uppercase vs Lowercase in RFC 2119 Key Words.
- RFC 8615 — Well-Known Uniform Resource Identifiers (URIs).
- RFC 8288 — Web Linking.
- RFC 9309 — Robots Exclusion Protocol.
- RFC 9116 — A File Format to Aid in Security Vulnerability Disclosure (security.txt).
- OpenID Connect Discovery — OpenID Foundation.
- Sitemaps Protocol — sitemaps.org.
- OpenAPI Specification — OpenAPI Initiative (Linux Foundation).
- Model Context Protocol (MCP) — open specification.
- Agent2Agent (A2A) Protocol — Linux Foundation.
- llms.txt — llmstxt.org community convention.

---

## Appendix C. About This Document

| Field | Value |
|---|---|
| Document type | Problem Statement |
| Document identifier | RFC-0000 |
| Project codename | ADP |
| Status | Working Draft — open for discussion |
| Related document | RFC-0001 |
| Author | Aybars Mete Keleş |
| Date | 27 June 2026 |

> This document is not an IETF document and is not published by any standards body. It is an independent working draft, published for open discussion, that adopts the writing conventions of an IETF Internet-Draft.
