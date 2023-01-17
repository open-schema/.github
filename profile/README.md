# Open Schema

One abstract computational model to rule a subset of them all!

**note:** This project is still under design. The scope has changed fairly significantly since the initial draft. The terminology is a work in progress, so there may be some inconsistencies in the documentation.

Want to see the profusely bleeding edge of Open Schema? Check out the volatile, rudimentary, experimental implementation [here](https://github.com/rachidlamouri/testing-platform#constraint-engine-demo).

## Description

Open Schema is an abstract semantic-driven computational model. That is, it describes how to process data while maintaining the purpose of that data at runtime. It is a [standard](https://xkcd.com/927/) for building systems that represent, describe, modify, validate, and generate data (or a subset therein). Open schema provides the high level patterns necessary to implement these five use cases without being tied to any one programming language or schema definition language.

## Key Takeaways

- There is no singular defining implementation of Open Schema
  - Open Schema is agnostic of any one language
  - Open Schema focuses on high level abstract patterns; not the specific implementation of those patterns
- Open Schema does not define a universal set of semantics
  - Semantics can only be defined when tied to a specific domain
  - An implementation of Open Schema must define its domain
  - For relative simplicity, Open Schema itself is currently constrained to the domain of digital systems
- Open Schema is designed to improve developer agility
  - A CPU is a finely tuned [Rube Goldberg machine](https://en.wikipedia.org/wiki/Rube_Goldberg_machine) that allows us to build abstract systems on top of it
  - Developers use computers to implement abstract solutations to definable problems
  - The Open Schema standard is focused on empowering developers to quickly iterate on language features and expand the interoperability of systems
  - Open schema is [Turing complete](https://en.wikipedia.org/wiki/Turing_completeness) [**citation needed**]
  - Open Schema is **not** designed to replace existing programming languages

## Potential Applications

- **Programming Languages**: Modern programming languages add data type semantics to the binary model of computation. Open Schema can be used to model these data type semantics and improve the static analysis of both [structural type systems](https://en.wikipedia.org/wiki/Structural_type_system) (eg [TypeScript](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)) and [nominal type systems](https://en.wikipedia.org/wiki/Nominal_type_system) (eg [C++](https://isocpp.org/))
- **Schema Definition Languages (SDLs)**: SDLs (eg [GraphQL](https://graphql.org/), [JSON Schema](https://json-schema.org/), [OpenApi](https://www.openapis.org/)) allow developers to describe data either within a system, or between systems. Open Schema allows developers to focus on enumerating and iterating on the features of an SDL without being limited by syntactic concerns.
- **Data Validation**: Open Schema abstracts the high level patterns around validating data so that existing systems (eg [JSON Schema](https://json-schema.org/)) can decouple their validation logic concerns from the specific semantics that their technology implements.
- **Mock Data Generation**: Open Schema abstracts the high level patterns around generating data so that data generation libraries (eg [JSON Schema Faker](https://github.com/json-schema-faker/json-schema-faker)) can drive their implementation from the enumerable features of the data description system (eg a programming language or SDL)
- **A Super Linter**: Linting is an application of data validation. That is, if you have a description of some system, then you can validate that an instance of the system matches the description. Since Open Schema abstracts the high level patterns around data validation, it can be used to implement a core linting pattern. This allows it to interface with existing linting implementations, and it permits those implementations to focus on domain-specific rules, and not the core pattern of processing rules.

## Open Schema Terminology

**Note:** This section could benefit from links between terminology. I'm experimenting with using Open Schema to lint the lack of links and incorrect links.

This section defines how the following terms should be interpreted within the context of Open Schema.

### Datum

A finite, non-empty set of computer memory. That is, one or more bits of information that is meant to be processed as a whole.

### Datum Instance

A datum that can be independently identified from other datum.

### Datum Instance Collection

A group of zero or more datum instances that can be processed as a whole. Because a datum instance collection can be empty, a datum instance collection is **not** inherently a datum, but it can be represented by a datum. That means that there is no universal implementation of a datum instance collection. Therefore, implementations of Open Schema must decide on one or more implementations of a datum instance collection (eg an object, set, tuple, array, map ...etc)

### Collection

A datum instance collection, or a collection of collections.

### Semantics

> the meaning of a word, phrase, sentence, or text

Since the word semantics does not have a distinguishable plural form, we will use the following notation to differentiate between the two forms:

- semantics(s.): singular
- semantics(p.): plural

### Datum Semantics(s.)

A practical concern around how to process a datum instance. This could be a technical concern, such as a data type, or an abstract concern, such as the real world concept that the datum represents.

### Datum Processor

Datum that can read and modify a collection when sent to something that can process the datum processor (ie. a CPU or another datum processor). A datum processor is said to have side effects when it modifies datum that another datum processor actively depends on.

| Datum Processor | Datum Processor Processor |
|---|---|
| Binary | CPU |
| Application | OS |
| File | Interpreter |
| Function | Language Runtime |

### Datum Semantics(s.) Processor

A datum processor that determines if a datum instance satisfies a datum semantics(s.). By definition, a datum semantics(s.) processor is a datum instance and therefore a datum.

### Datum Semantics(s.) Processor Result

A datum instance that represents the outcome of processing a datum instance through a datum semantics(s.) processor. The most trivial implemenation is a single bit that indicates success or failure.

### The Null Datum Semantics(s.) Processor Result

A special datum semantics(s.) processor result that indicates that a datum instance has not yet been processed by a datum semantics(s.) processor.

### Collection Locator

A datum that is used to find a collection.

### Datum Instance Locator

A collection locator that can be used to find a collection with exactly one datum instance.

### Canonical Datum Instance Locator

The primary datum instance locator for a datum instance.

### Canonical Datum Semantics(s.) Locator

The canonical datum instance locator for a datum semantics(s.) processor. It can also be used to refer to a particular datum semantics(s.).

### Identifiable Datum semantics(s.) processor Result

A collection that contains a datum semantics(s.) processor result and a canonical datum semantics(s.) locator.

### Datum Instance Semantics(s.) Results Collection

A collection that contains a canonical datum instance locator as well as zero or more related identifiable datum semantics(s.) processor results. Note that a datum instance semantics(s.) results collection does not actually contain the datum instance, nor does it need to.

### Identifiable Datum Instance

A collection that contains a datum instance and a canonical datum instance locator.

### Datum Instance Alias

A collection that contains a canonical datum instance locator and a non-canonical datum instance locator for the same datum instance.

### Datum Instance Predicate

A collection that contains a canonical datum instance locator, and a canonical datum semantics(s.) locator.

### Datum Semantics(s.) Processor Result Processor

A datum processor that takes a datum semantics(s.) processor result and a canonical datum instance locator and either produces an empty collection or a collection with a datum instance predicate.

### Conditional Datum Semantics(s.) Processor

A datum semantics(s.) processor that should only be applied to a datum instance if a collection of datum instance predicates is satisfied. Technincally all datum semantics(s.) processors are conditional processors because the empty collection of datum instance predicates is always satisifed.

### Datum Instance Configuration

A collection that contains an identifiable datum instance, zero or more datum instance aliases, and zero or more datum instance predicates. For clarity: all data in the collection must be related to the same datum instance.

### Datum Instance Configuration Collection Builder

A datum processor that takes a datum instance configuration collection, and creates a datum instance configuration collection.

### Datum Semantic(s.) Configuration

A collection that contains a datum semantics(s.) identifier, and a collection locator. This allows the associated datum semantics(s.) processor to be applied to all datum instances that can be found by the collection locator.

### Datum Instance Configuration Collection Builder Configuration

A collection that contains a collection of collection locators, a collection of datum instance predicates, and a datum instance configuration collection builder that can process the collection of datum instances that can be found by the collection of collection locators.

### Builder Configuration

Alias for a datum instance configuration collection builder configuration.

### Engine

A datum processor that repeatedly performs one or more operations.

### Data Representation Engine

A datum processor that takes a collection of builder configurations, a collection of datum instance predicates and a collection locator, and produces a collection of datum instance configuration collections. These resulting collections and their locators can be fed back into the system. For builder configurations with non-empty datum collection predicate collections, it will only invoke the builder if the predicates are met.

### Data Description Engine

A datum processor that takes some data and transforms it into a datum semantic(s.) configuration.

### Data Validation Engine

A datum processor that takes a builder configuration collection, a datum semantics(s.) configuration collection and uses a data representation engine to continuously produce datum instances and apply datum semantics(s.) to them.

### Data Generation Engine

A data representation engine whose input builder configurations are designed around datum semantics(s.) configurations. That is, it takes a collection of datum semantics(s.) configurations and builds a datum instance.

## History and Motivation

```md
TL;DR: Mistakes were made
```

1. In hindsight, the ideas behind this project go way back. I was learning full stack web development and basic devops when I ran into the problem of keeping deployed and local database schemas in sync. At the time, I didn't know how to use database migrations to keep deployed databases in sync with my code features. So, I experimented with using database queries to get the structure of each system, to dump the structure to a file, run a diff on the file, and drive a manual process to keep them in sync. I know it sounds bad: I'm in the future also.
2. At a different point in my career, I was focusing on adding test patterns to a frontend system to keep it in sync with multiple backend systems that were each governed by various JSON Schemas. As a side note, it wouldn't have mattered if we had been using Open API or GraphQL or some other technology, because the resulting problems would have been the same. I was trying to get ahead of the fact that when developers can't readily generate mock data, they will copy chunks of data from test API calls and paste into a code file. This in turn, makes the system impossible to maintain. As a result:
    1. I created [schema-to-generator](https://www.npmjs.com/package/@randograms/schema-to-generator): a wrapper on top of [json-schema-faker](https://www.npmjs.com/package/json-schema-faker) that allows developers to create entire valid objects (or other data types) while only having to specify a subset of the properties. This means that tests can remain lightweight, that is focused on the data that is relevant to the test, while evolving with the external schemas.
    2. In creating `schema-to-generator`, I found that a subset of bugs were coming from `json-schema-faker`. After digging into `json-schema-faker`, I realized that it lacked a driving algorithm for creating data. Therefore, I created [schema-to-data](https://www.npmjs.com/package/@randograms/schema-to-data) which follows a core algorithm ([see related diagrams](https://github.com/randograms/schema-to-data/blob/master/docs/developerGuide.md#diagrams)) to make sure that it creates valid data.
    3. After creating `schema-to-data`, I experimented with something I called `json-schema-script`: A [Babel](https://babeljs.io/) plugin that transpiles JSON Schema function annotations as function decorators. That is, you use JSON Schema to annotate the constraints on the inputs and outputs of a function, so that the function gets transpiled to a higher order function that dynamically validates the inputs and outputs of the wrapped function. Again, I'm in the future also. **Note**: my `json-schema-script` implementation is lost in the history of a private repository (RIP `json-schema-script`, 2020-2022).
    4. After realizing that I was essentially making a new programming language, I decided to temporarily stop reinventing the wheel, and learn a programming language that adds useful static constraints: TypeScript!
3. From the experience I gained from the previous point, I came to some interesting realizations:
    - If I had continued focusing on JSON Schema, then I would always be limited by the domain of JSON and the capabilities of JSON Schema.
    - JSON Schema is **only** focused on the annotation and validation of data ([see JSON Schema](https://json-schema.org/)), **not** the generation of data (see [JSON Type Definitions](https://jsontypedef.com/)). Therefore, my approach was fundamentally flawed.
    - It's difficult to improve on existing systems when they don't have enumerable features. Making `schema-to-data` was a pain, because I never understood the full scope of JSON Schema keywords that needed to be implemented, and my implementation couldn't rapidly scale as JSON Schema evolved.
    - [IMHO](https://en.wiktionary.org/wiki/IMHO), although TypeScript is amazing, it just introduces a new set of proprietary problems.
        - The type errors are kind of a pain to read, and from my perspective, they appear to be from the perspective of the language maintainers not developers using TypeScript.
        - It would be greatly beneficial if type declarations could have code blocks, so that my types don't have to be very long, complicated expressions.
        - I can't easily unit test parameterized types which makes complicated types harder to maintain.
        - The syntax for parameterized types feels unnecessarily coupled to the implementation constraints of processing parameterized types.
        - It's hard to find an offical enumerated list of TypeScript features to keep up with the latest features or to build supplemental tooling that takes advantage of the latest features.
    - "Just use language X" is an unhelpful response to gripes with existing languages. It shows that developers couple syntactic features to the goals that the language solves. We should be able to rapidly iterate on how we input information to a system, without affecting how the system processes the inputs.
4. I have an ongoing private project that I use to iterate and expand on my own personal developer experience. The project is an n-tier application, and I've been continuously thinking about how I can maintain the integrity of data as it moves between each layer of the system. That is, I wanted to capture which technologies add and remove constraints, and how I can use the definitions of those constraints to drive the interoperability of each part of the system. The evolution of this project proceeded in parallel to the experiences outlined above, and has contributed to where Open Schema is today. I hope that Open Schema will allow me to model my application as a whole, and to drive the implementation of each layer via the technology that is most suited for that layer.
