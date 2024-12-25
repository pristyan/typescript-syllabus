# Module 6: Advanced Topics and Best Practices (Ongoing)

This module covers more advanced TypeScript features and best practices for writing maintainable and efficient TypeScript code. This is an "ongoing" module because these are topics you'll likely continue to learn and refine as you gain more experience.

## 6.1 Declaration Merging

*   **Merging Declarations of Interfaces, Classes, and Namespaces:** TypeScript allows you to merge declarations with the same name. This is useful for extending existing types or adding properties to modules.

    ```typescript
    interface Animal {
      name: string;
    }

    interface Animal { // Merging with the previous interface
      age: number;
    }

    const myAnimal: Animal = {
      name: "Dog",
      age: 5,
    };

    // Example with namespaces (less common now):
    namespace MyNamespace {
        export let value = "initial value";
    }

    namespace MyNamespace {
        export function getValue() { return value; }
    }

    console.log(MyNamespace.value);
    console.log(MyNamespace.getValue());
    ```

## 6.2 Decorators

*   **Adding Metadata to Classes, Methods, and Properties:** Decorators are a way to add metadata or modify the behavior of classes, methods, accessors, properties, and parameters. They use the `@` symbol. (Requires `"experimentalDecorators": true` in `tsconfig.json`)

    ```typescript
    function logClass(constructor: Function) {
      console.log(`Class ${constructor.name} was created.`);
    }

    @logClass
    class MyClass {
      constructor() {}
    }

    // Example with Method decorator
    function logMethod(target: any, key: string, descriptor: PropertyDescriptor) {
        const originalMethod = descriptor.value;

        descriptor.value = function (...args: any[]) {
            console.log("Before method call");
            const result = originalMethod.apply(this, args);
            console.log("After method call");
            return result;
        }
    }

    class Calculator {
        @logMethod
        add(a: number, b: number) {
            return a + b;
        }
    }

    const calculator = new Calculator();
    calculator.add(2, 3);
    ```

## 6.3 Mixins

*   **Creating Reusable Code Through Composition:** Mixins provide a way to reuse code across multiple classes without using traditional inheritance. They use intersection types and generic functions.

    ```typescript
    function applyMixins(derivedCtor: any, baseCtors: any[]) {
        baseCtors.forEach(baseCtor => {
            Object.getOwnPropertyNames(baseCtor.prototype).forEach(name => {
                Object.defineProperty(derivedCtor.prototype, name, Object.getOwnPropertyDescriptor(baseCtor.prototype, name) || Object.create(null));
            });
        });
    }

    class Disposable {
        isDisposed: boolean = false;
        dispose() {
            this.isDisposed = true;
        }
    }

    class Activatable {
        isActive: boolean = false;
        activate() {
            this.isActive = true;
        }
    }

    class SmartObject implements Disposable, Activatable {
        constructor() {
            setInterval(() => console.log(this.isDisposed + " : " + this.isActive), 500);
        }

        isDisposed: boolean = false;
        dispose!: () => void;
        isActive: boolean = false;
        activate!: () => void;
    }
    applyMixins(SmartObject, [Disposable, Activatable]);

    let smartObj = new SmartObject();
    setTimeout(() => smartObj.activate(), 1000);
    setTimeout(() => smartObj.dispose(), 2000);
    ```

## 6.4 Type-Driven Development

*   **Designing Your Code Around Types:** Type-Driven Development (TDD) emphasizes defining types first and then implementing the code to satisfy those types. This can lead to more robust and well-structured code.

## 6.5 Performance Optimization

*   **Tips for Writing Performant TypeScript Code:**
    *   Avoid using `any` excessively. It disables type checking and can lead to runtime errors and performance issues.
    *   Use interfaces and types effectively to define clear contracts and improve code readability.
    *   Be mindful of type inference and use explicit type annotations when necessary.
    *   Use utility types to avoid redundant type definitions.

## 6.6 Integration with Other Tools

*   **ESLint:** Use ESLint with a TypeScript parser (`@typescript-eslint/parser`) to lint your TypeScript code and enforce coding style and best practices.
*   **Prettier:** Use Prettier to format your code consistently.
*   **Testing frameworks (Jest, Mocha, etc.):** Use testing frameworks with appropriate type definitions to write type-safe tests.
