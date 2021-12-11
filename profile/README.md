# Open Schema

One abstract schema definition language (SDL) to rule them all.

## The Open Schema Document (OSD)

*Note*: This document does not exist ... yet.

The OSD is a specification for how to write any language-agnostic SDL that can include definitions for data types, data structures AND data constraints. The OSD can be used to define any domain-specific SDL such as:

- A serialized data validation schema: [json-schema](https://json-schema.org/)
- An API schema: [GraphQL](https://graphql.org/), [OpenApi](https://www.openapis.org/)
- A [structural type system](https://en.wikipedia.org/wiki/Structural_type_system): [typescript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html), [flow](https://flow.org/en/), [RBS](https://github.com/ruby/rbs), [Sorbet](https://sorbet.org/),
- A [nominal type system](https://en.wikipedia.org/wiki/Nominal_type_system): [C++](https://isocpp.org/), [C#](https://docs.microsoft.com/en-us/dotnet/csharp/), [Java](https://docs.oracle.com/en/java/), [Rust](https://www.rust-lang.org/learn)

The OSD should not have a single implementation, as that would imply a universally compatible definition for any data type or data validation system. Therefore an SDL that follows the OSD must restrict its domain. Over time it can be expected for certain SDLs to dominate certain domains, but an abstract OSD will never restrict the potential for the community to handle new domain concerns.

The OSD can be used to write an Open Schema Schema Definition Language (OSSDL) which is then used to define various Open Schema Schemas (OSS). Since an OSSDL encompasses all of the data concerns of a domain, a single OSS of an OSSDL would encompass the concerns of a subdomain of the OSSDL's domain.

*Note*: The name "Open Schema Document" was chosen in favor of "Open Schema Specification" as the acronym OSS would conflict with "Open Schema Schema".

## Motivation

The author wishes to define schemas for various layers of an n-tier application to separate the data integrity concerns of each layer. These schemas would then be used to enforce data concerns within code, enforce data concerns within tests, generate mock data structures for tests, mock entire layers in tests, derive schemas for other layers, and derive documentation for each layer and the application as a whole. By using an OSSDL for the application domain, the OSSs for any layer can be ported to the subdomain SDL of that layer. That is, the application would have an SDL that encompasses the needs of the SDLs within its tech stack. In turn, this enables the tech stack to evolve without losing data integrity concerns at any layer. Currently, the author has to manage several independent SDLs with various levels of redundant information, as well as the assorted incomplete tooling to transform schemas from one SDL to another. This makes them sad.

## Plan

The current plan is to write a document that abstracts the core ideas behind [json-schema](https://json-schema.org/) without focusing on data serialization concerns. That is, it will provide a system to define keywords, their configuration and how that configuration should be interpreted within any specific domain.

The OSD does not necessarily need to define a specific format for an OSSDL. That is, an OSSDL does not have to be able to be converted to a JSON document or any one format. Documentation for a specific OSSDL can include what format the OSSDL should take. The implications of this still need to be explored.

The specifics of writing the specification are TBD.
