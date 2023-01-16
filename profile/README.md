# Open Schema

One abstract computational model to rule a subset of them all!

**note:** This project is still under design. The scope has changed fairly significantly since the initial draft. The terminology is a work in progress, so there may be some inconsistencies in the documentation.

## Description

Open Schema is an abstract semantic-driven computational model. That is, it describes how to process data while maintaining the purpose of that data at runtime. It is a [standard](https://xkcd.com/927/) for building systems that represent, describe, modify, validate, and generate data (or a subset therein). Open schema provides the high level patterns necessary to implement these five use cases without being tied to any one programming language or schema definition language.

## Key Takeaways

- Open schema is [Turing complete](https://en.wikipedia.org/wiki/Turing_completeness) [**citation needed**]
- There is no singular defining implementation of Open Schema
  - Open Schema is agnostic of any one language
  - Open Schema focuses on high level abstract patterns; not the specific implementation of those patterns
- Open Schema does not define a universal set of semantics
  - Semantics can only be defined when tied to a specific domain
  - An implementation of Open Schema must define its domain
  - For relative simplicity, Open Schema itself is currently constrained to the domain of digital systems
- Open Schema can improve developer agility
  - A CPU is a finely tuned [Rube Goldberg machine](https://en.wikipedia.org/wiki/Rube_Goldberg_machine) that allows us to build abstract systems on top of it
  - Developers use computers to implement abstract solutations to definable problems
  - The Open Schema standard is focused on empowering developers to quickly iterate on language features and expand the interoperability of systems

## Potential Applications

- **Programming Languages**: Modern programming languages add data type semantics to the binary model of computation. Open Schema can be used to model these data type semantics and improve the static analysis of both [structural type systems](https://en.wikipedia.org/wiki/Structural_type_system) (eg [TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)) and [nominal type systems](https://en.wikipedia.org/wiki/Nominal_type_system) (eg [C++](https://isocpp.org/))
- **Schema Definition Languages (SDLs)**: SDLs (eg [GraphQL](https://graphql.org/), [JSON Schema](https://json-schema.org/), [OpenApi](https://www.openapis.org/)) allow developers to describe data either within a system, or between systems. Open Schema allows developers to focus on enumerating and iterating on the features of an SDL without being limited by syntactic concerns.
- **Data Validation**: Open Schema abstracts the high level patterns around validating data so that existing systems (eg [JSON Schema](https://json-schema.org/)) can decouple their validation logic concerns from the specific semantics that their technology implements.
- **Mock Data Generation**: Open Schema abstracts the high level patterns around generating data so that data generation libraries (eg [JSON Schema Faker](https://github.com/json-schema-faker/json-schema-faker)) can drive their implementation from the enumerable features of the data description system (eg a programming language or SDL)
- **A Super Linter**: Linting is an application of data validation. That is, if you have a description of some system, then you can validate that an instance of the system matches the description. Since Open Schema abstracts the high level patterns around data validation, it can be used to implement a core linting pattern. This allows it to interface with existing linting implementations, and it permits those implementations to focus on domain-specific rules, and not the core pattern of processing rules.

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
