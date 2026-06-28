# Discussion 0002: Scope Boundaries

> This is a discussion seed, not a specification.

This project intentionally focuses on service-interface discovery.

It does not currently define:

- capability semantics
- intent semantics
- authentication
- authorization
- trust
- pricing
- policy semantics
- agent runtime behavior
- service ranking or selection

## Questions

1. Is the current scope too narrow, too broad, or correct?
2. Which topics should remain explicitly out of scope for RFC-0001?
3. Which topics should be future extension documents?
4. Are any non-goals currently unclear?

## Current principle

Discovery should answer:

> Where are the machine-consumable interfaces?

It should not answer:

> Which service should the agent choose?
> Is this service trustworthy?
> What is the business meaning of every capability?
