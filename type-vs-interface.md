# Type Aliases vs. Interfaces in TypeScript

## Introduction

Type aliases and interfaces both give names to types, making declarations easier to read and reuse. For ordinary object shapes, they often look interchangeable. Their differences matter when a program needs unions, extension, or an API that other developers may augment.

## Detailed Comparison

An interface describes an object contract and can be extended with `extends`. Interfaces also support declaration merging: compatible declarations with the same name are combined. This is useful for library authors who intentionally allow consumers to add fields to a public type.

```ts
interface User {
  id: number;
}

interface Admin extends User {
  permissions: string[];
}
```

A type alias can name object shapes too, but its range is broader: it can represent primitives, unions, tuples, and intersections. For example, a value that is either a number or a string is naturally expressed as a union alias.

```ts
type Identifier = number | string;
type UserLabel = User & { label: string };
```

Unlike interfaces, aliases do not merge when redeclared. That helps catch accidental duplicate declarations, though it also means aliases are not the right tool for declaration augmentation. For object-oriented contracts, `interface` often communicates intent clearly and supports extension. For composed or non-object types, `type` is usually the direct choice. Neither is universally superior; consistency within a codebase is also important.

## Conclusion

Choose an interface for extensible object contracts and a type alias for unions, tuples, intersections, or other type expressions. Let the shape and extension needs guide the decision.
