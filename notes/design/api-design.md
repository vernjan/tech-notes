# API Design

## Sources
- [Design First or Code First: What’s the Best Approach to API Development?](https://swagger.io/blog/api-design/design-first-or-code-first-api-development/)
- [OpenAPI - Getting started](https://oai.github.io/Documentation/start-here.html)

## Approaches

### Design first
- start with a contract (OpenAPI), then generate code
- good for robust public APIs
    - improves developer experience
    - serves as documentation

### Code first
- generate contract from code
- good for (smaller) internal APIs
    - it's faster to start working with

## JSON compatibility
- see [compatibility](system-design/compatibility.md)

### Backward-compatible changes
_i.e. changes on the consumer side_

- adding a field with a default value
- adding an optional field
- removing a field
- widening a numerical type
- adding a value to an enum

### Forward-compatible changes
_i.e. changes on the producer side_

- adding a new filed (assuming consumers ignore unknown field)
- adding a value to an enum (assuming consumers can handle “else” case)
- narrowing a numerical type
- removing a value from an enum string

## OpenAPI
- industry standard for RESTful API design
    - formalize any HTTP-like API (endpoints, requests schema, response schema)
- human and machine-readable
- specification maintained by top companies
    - **Swagger** - tools implementing OpenAPI by Smartbear
- [lots of tools](https://openapi.tools/) to support automation
    - code generation
    - docs generation
    - validation
    - automated testing