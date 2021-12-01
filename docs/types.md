# Bicep type system

This is an attempt to rationalize and fully describe the semantics of the Bicep type system in a more rigourous way. Bicep today has a powerful type system, but the expressiveness of its type system is not fully exposed to users. As an example, users can declare a parameter using a type like `object` but cannot define their own strongly typed objects.

The goal of this document is to produce a design and roadmap for capturing Bicep's type semantics in three forms:

- How users declare and reference types in Bicep code.
- How type information is persisted in ARM-JSON for tools to process.
- How type information is imported into the Bicep compiler (FFI).

## Considerations

We need to consider carefully how Bicep's types are represented in both the Bicep language as well as the ARM-JSON language, as every Bicep template is compiled to ARM-JSON. ARM-JSON (in its current form) is strongly typed for parameters and outputs, and untyped for the processing of resource bodies and intermediate expressions. 

In its role as an IL, ARM-JSON imposes some limitations. Parameters and ouputs must be typed as **one** of:

- array
- bool
- int
- object
- secureObject
- secureString
- string

As an example of a limitation, a Bicep type might be `any` or a union of `string` and `integer`. This cannot be represented as an ARM-JSON parameter or output. Note that `object` refers to a JSON-like object. It is not a *top* type like `object` in C# and Java.

Any Bicep type must be lowered/serialized to an appropriate ARM-JSON type when is used as a parameter or output. It is for these use cases that we need to capture **both** the best ARM-JSON type for the deployment engine as well as the Bicep language semantics for tooling.

## Bring out the types

TODO: type lattice diagram

### Primitives

### Any

### Arrays

### Objects

### Null

### Never

### Resources

### Unions

### Functions