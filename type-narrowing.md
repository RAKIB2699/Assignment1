# Type Narrowing in TypeScript

## Introduction

Type narrowing is the process of refining a broad type into a more specific type after checking a runtime condition. It lets TypeScript verify that an operation is safe without requiring a type assertion. Narrowing is especially useful when a function accepts unions or values from external sources.

## Detailed Examples

The `typeof` operator distinguishes primitive types. In the first branch below, TypeScript knows `input` is a string, so string methods are available; in the other branch, it is a number.

```ts
function describe(input: string | number): string {
  if (typeof input === "string") return input.trim();
  return input.toFixed(2);
}
```

For class instances, `instanceof` checks an object's prototype chain. After the condition succeeds, the variable is narrowed to that class and its methods can be called safely.

```ts
class Dog {
  bark(): string {
    return "woof";
  }
}

function sound(value: Dog | Date): string {
  if (value instanceof Dog) return value.bark();
  return value.toISOString();
}
```

The `in` operator checks whether a property exists on an object. It works well with discriminated object alternatives when those alternatives have distinct fields.

```ts
type EmailMessage = { email: string };
type SmsMessage = { phone: string };

function recipient(message: EmailMessage | SmsMessage): string {
  if ("email" in message) return message.email;
  return message.phone;
}
```

These checks do more than affect runtime behavior: TypeScript tracks their results through each branch and rejects property access that is not valid for the narrowed type. Prefer checks that match the actual data model, and handle every remaining case explicitly.

## Conclusion

`typeof`, `instanceof`, and `in` are practical tools for narrowing values at runtime while preserving compile-time safety. Use them to make union-handling code clear and dependable.
