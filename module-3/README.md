# Module 3: Advanced Types and Generics

This module covers more advanced type system features in TypeScript, including generics, conditional types, mapped types, and utility types.

## 3.1 Generics

*   **Creating Reusable Components and Functions:** Generics allow you to write code that can work with a variety of types without sacrificing type safety.

    ```typescript
    function identity<T>(arg: T): T {
      return arg;
    }

    let myString: string = identity<string>("hello");
    let myNumber: number = identity<number>(123);
    let myBoolean: boolean = identity<boolean>(true);
    ```

*   **Generic Interfaces and Classes:**

    ```typescript
    interface Box<T> {
      value: T;
    }

    let numberBox: Box<number> = { value: 10 };
    let stringBox: Box<string> = { value: "hello" };

    class DataHolder<T> {
      data: T;
      constructor(data: T) {
        this.data = data
      }
    }

    let dataHolderNumber = new DataHolder<number>(10);
    let dataHolderString = new DataHolder<string>("hello");
    ```

*   **Type Parameters and Constraints:** You can constrain the types that a generic type can accept.

    ```typescript
    interface Lengthy {
      length: number;
    }

    function logLength<T extends Lengthy>(arg: T): void {
      console.log(arg.length);
    }

    logLength("hello"); // Works because string has a 'length' property
    logLength([1, 2, 3]); // Works because arrays have a 'length' property
    // logLength(123); // Error: Argument of type 'number' is not assignable to parameter of type 'Lengthy'.
    ```

## 3.2 Keyof Operator

*   **Getting the Keys of a Type:** The `keyof` operator allows you to get a union of the keys of a type.

    ```typescript
    interface Person {
      name: string;
      age: number;
    }

    type PersonKeys = keyof Person; // "name" | "age"

    function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
        return obj[key];
    }

    const person: Person = {name: "John", age: 30}
    const personName = getProperty(person, "name"); // type of personName is string
    const personAge = getProperty(person, "age"); // type of personAge is number

    ```

## 3.3 Typeof Operator

*   **Getting the Type of a JavaScript Value:** The `typeof` operator in TypeScript is the same as in JavaScript, but it can also be used in type contexts.

    ```typescript
    let message = "hello";
    type MessageType = typeof message; // string

    const obj = {a: 1, b: "hello"}
    type ObjType = typeof obj; // {a: number, b: string}
    ```

## 3.4 Conditional Types

*   **Creating Types that Depend on Other Types:** Conditional types allow you to create types that are determined based on a condition.

    ```typescript
    type IsString<T> = T extends string ? "yes" : "no";

    type StringResult = IsString<string>; // "yes"
    type NumberResult = IsString<number>; // "no"

    type TypeName<T> =
        T extends string ? "string" :
        T extends number ? "number" :
        T extends boolean ? "boolean" :
        T extends undefined ? "undefined" :
        T extends Function ? "function" :
        "object";

    type T0 = TypeName<string>;  // "string"
    type T1 = TypeName<"a">;  // "string"
    type T2 = TypeName<() => void>;  // "function"
    type T3 = TypeName<string[]>;  // "object"
    ```

## 3.5 Mapped Types

*   **Transforming Existing Types:** Mapped types allow you to create new types by transforming existing ones.

    ```typescript
    interface Person {
      name: string;
      age: number;
    }

    type ReadonlyPerson = Readonly<Person>; // All properties are now readonly

    type PartialPerson = Partial<Person>; // All properties are now optional

    type PersonKeys = keyof Person; // "name" | "age"
    type NullablePerson = {
        [P in PersonKeys]: Person[P] | null
    }
    ```

## 3.6 Utility Types

TypeScript provides several built-in utility types that make type manipulation easier:

*   `Partial<T>`: Makes all properties of `T` optional.
*   `Readonly<T>`: Makes all properties of `T` readonly.
*   `Record<K, T>`: Creates a type with keys of type `K` and values of type `T`.
*   `Pick<T, K>`: Creates a type by picking specific properties `K` from `T`.
*   `Omit<T, K>`: Creates a type by omitting specific properties `K` from `T`.
*   `Exclude<T, U>`: Excludes types assignable to `U` from `T`.
*   `Extract<T, U>`: Extracts types assignable to `U` from `T`.
*   `NonNullable<T>`: Excludes `null` and `undefined` from `T`.
*   `ReturnType<T>`: Gets the return type of a function type `T`.
*   `InstanceType<T>`: Gets the instance type of a constructor function type `T`.

    ```typescript
    interface Todo {
      title: string;
      description: string;
      completed: boolean;
    }

    type TodoPreview = Pick<Todo, "title" | "completed">;

    const preview: TodoPreview = {
      title: "Clean room",
      completed: false,
    };
    ```

## 3.7 Discriminated Unions

*   **Creating Types that are Easily Distinguishable at Runtime:** Discriminated unions (also known as tagged unions or algebraic data types) are useful for representing values that can have different shapes. They use a common "discriminator" property to distinguish between the different types.

    ```typescript
    interface Square {
      kind: "square";
      size: number;
    }

    interface Circle {
      kind: "circle";
      radius: number;
    }

    type Shape = Square | Circle;

    function area(s: Shape): number {
      switch (s.kind) {
        case "square": return s.size * s.size;
        case "circle": return Math.PI * s.radius ** 2;
      }
    }
    ```
