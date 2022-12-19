# Open Schema

A platform for integrating schemas across domains. It contains the specification for an interoperable constraint engine.

**note** This project is still under design. The scope has changed fairly significantly since the initial draft. The terminology is a work in progress, so there may be some inconsistencies in the documentation.

## Description

This project aims to define how to process a set of constraints against a set of targets regardless of the schema definition language (SDL) used when defining the constraints and targets. In doing so, this project can facilitate the interoperability of other systems such as:

- Serialized data validation schemas: [json-schema](https://json-schema.org/)
- API schemas: [GraphQL](https://graphql.org/), [OpenApi](https://www.openapis.org/)
- [Structural type systems](https://en.wikipedia.org/wiki/Structural_type_system): [typescript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html), [flow](https://flow.org/en/), [RBS](https://github.com/ruby/rbs), [Sorbet](https://sorbet.org/),
- [Nominal type systems](https://en.wikipedia.org/wiki/Nominal_type_system): [C++](https://isocpp.org/), [C#](https://docs.microsoft.com/en-us/dotnet/csharp/), [Java](https://docs.oracle.com/en/java/), [Rust](https://www.rust-lang.org/learn)
- Static analysis tooling
- Repository convention tooling

## Benefits

- It's agnostic of data input: This allows systems to define SDLs that fit their unique needs
- It focuses on how to define constraints in the abstract: This allows the system to scale to any set of constraints. For example: json-schema is concerned with structuring schemas, definitions of reserved keywords, and handling non-reserved keywords, which resulted in a larger scope of responsibility, and conflicting implementations of keywords.
    - Ideally this means that any existing SDL and its constraints can be ported to and from open-schema
- It's designed to be platform independent: It should be possible to build the core constraint engine in any language, and have it interface with constraints implemented in any other languages. It also proposes patterns for building constraint adapters, that can handle the domain concerns of running several unrelated process together efficiently.
    - For example you might use a core engine written in Rust, but have TypeScript constraints that you want to run under one runtime environment
- Constraints will be indexed: We will use [UUID version 4](https://en.wikipedia.org/wiki/Universally_unique_identifier#Version_4_(random)) to create unique identifiers for constraints. This allows different systems to know that they are interfacing with an implementation of the expected constraint. It also enables the enumeration of constraints, so that new engines and constraint implementations can check their validity against existing engines and implementations.
    - We can define or use an existing definition for an id-hash that is a shorter version of a UUID V4 that is slightly easier to read, and has a 1-1 mapping to UUID V4
    - Constraints will also have a human readble name, but names are not canonical
    - We could also have a registry of constraint implementations and unique constraint definitions
- Different implementations can serve different use cases: For example, some workflows might need an atomic and fast paced engine to provide immediate feedback in an editor, while others might need an asynchronus workflow such as aggregating status updates across the internet.

## Terminology (WIP)

### Task

Something that takes zero or more inputs and produces zero or more outputs. Can be implemented by (but is not necessarily limited to) a function or a process.

### Target Concept

A thing that can be asserted on. It can be tangible or abstract. It can also be a subset or sub-property of another target concept.

### Target Structure

The data structure for a target concept.

### Target Instance

The independent in-memory information about a specific occurence of a target concept that matches a defined target structure for that concept.

### Target Path

A serializeable reference to a target instance.

### Target Instantiator

A task that takes zero or more target instances and creates a target instance and a target path for that instance.

### Target Path Instantiator

A task that creates an alternate target path for a given target instance

### Static Target Instance

For lack of a better word: a "hardcoded" target instance.

### Root Target Instance

Either a static target instance, or a target instance created by a target instantiator that took 0 inputs.

### Derived Target Instance

A target instance created by a target instantiator that took one or more inputs.

### Rule

A task that makes an assertion on a target instance. Rules can also define a dependency on another rule against the same target structure or another target along a target instance's target path.

**TBD**: Creating all target instances up front could eat up a lot of memory and have a really poor performance, so I'm still designing a way for targets to be derived after a rule passes when rules are dependent on one another.

### Rule Configuration

Information that binds a rule to a target path. This means that a rule is not automatically applied to all instances of its related target concept.

### Target Engine

A task that takes a set of target instantiators and static target instances and creates derived target instances with target paths.

### Rule Engine

A task that takes a rule configuration, a set of rules, and a set of target instances with target paths, and applies all rules in dependent order

### Presentation Engine

A task that processes the output of other engines to produce a readible output with actionable information.

### Constraint Engine

A task that manages one or more target engines, one or more rule engines, and one or more presentation engines to dynamically instantiate targets, apply rules to the targets, and present the results of the applied rules.

## Motivation

I want to define schemas for various layers of an n-tier application to separate the data integrity concerns of each layer. These schemas would then be used to enforce data concerns within code, enforce data concerns within tests, generate mock data structures for tests, mock entire layers in tests, derive schemas for other layers, and derive documentation for each layer and the application as a whole. On top of this, I want to enforce various constraints on the structure of my repositories to drive enforceable conventions.
