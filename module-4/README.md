# Module 4: Working with Classes and Modules

This module covers classes, a fundamental concept in object-oriented programming, and modules, which help organize and structure larger TypeScript projects.

## 4.1 Classes

*   **Defining Classes:** Classes are blueprints for creating objects. They define properties (data) and methods (actions) that objects of that class will have.

    ```typescript
    class Animal {
      name: string;
      constructor(name: string) {
        this.name = name;
      }

      makeSound() {
        console.log("Generic animal sound");
      }
    }

    const myAnimal = new Animal("Generic Animal");
    myAnimal.makeSound(); // Output: Generic animal sound
    ```

*   **Constructors:** The `constructor` is a special method that is called when a new object of the class is created. It's used to initialize the object's properties.

*   **Methods:** Functions defined within a class.

*   **Properties:** Variables defined within a class.

*   **Access Modifiers (public, private, protected):**

    *   `public` (default): Members are accessible from anywhere.
    *   `private`: Members are only accessible within the class itself.
    *   `protected`: Members are accessible within the class and its subclasses (inherited classes).

    ```typescript
    class Dog extends Animal {
      private breed: string;

      constructor(name: string, breed: string) {
        super(name); // Call the parent class constructor
        this.breed = breed;
      }

      makeSound() {
        console.log("Woof!");
      }

      getBreed(): string {
          return this.breed;
      }
    }

    const myDog = new Dog("Buddy", "Golden Retriever");
    myDog.makeSound(); // Output: Woof!
    // myDog.breed; // Error: Property 'breed' is private and only accessible within class 'Dog'.
    console.log(myDog.getBreed()); // Output: Golden Retriever
    ```

*   **Inheritance:** Creating new classes based on existing classes. The new class inherits the properties and methods of the parent class. Use `extends` keyword.

*   **Interfaces:** Interfaces can be used to define contracts that classes must adhere to. Use `implements` keyword.

    ```typescript
    interface Speakable {
        speak(): void;
    }

    class Cat implements Speakable {
        speak(): void {
            console.log("Meow!");
        }
    }
    ```

*   **Abstract Classes:** Classes that cannot be instantiated directly. They serve as blueprints for other classes. Use `abstract` keyword.

    ```typescript
    abstract class Shape {
        abstract getArea(): number;
    }

    class Circle extends Shape {
        radius: number;
        constructor(radius: number) {
            super();
            this.radius = radius;
        }
        getArea(): number {
            return Math.PI * this.radius * this.radius;
        }
    }

    // const myShape = new Shape(); // Error: Cannot create an instance of an abstract class.
    const myCircle = new Circle(5);
    console.log(myCircle.getArea()); // Output: 78.53981633974483
    ```

## 4.2 Modules

*   **Organizing Code into Modules:** Modules allow you to split your code into reusable units. This improves code organization, maintainability, and reusability.

*   **`import` and `export` Statements:**

    *   `export`: Makes a variable, function, class, or interface available to other modules.
        *   `export default`: Exports a single default export.
        *   Named exports: Exports multiple values with their names.

    *   `import`: Imports values from other modules.

    ```typescript
    // math.ts
    export function add(a: number, b: number): number {
        return a + b;
    }

    export const PI = 3.14159;

    export default function subtract(a: number, b: number): number {
        return a - b;
    }

    // main.ts
    import subtract, { add, PI } from './math';

    console.log(add(5, 3)); // Output: 8
    console.log(PI);      // Output: 3.14159
    console.log(subtract(10, 4)); // Output: 6
    ```

*   **Working with Different Module Systems (CommonJS, ES modules):** TypeScript supports both CommonJS (used in Node.js) and ES modules (the standard module system for JavaScript). Modern projects generally use ES modules. The `module` compiler option in `tsconfig.json` controls which module system is used.

## 4.3 Namespaces (Less common in modern TS)

*   **Organizing Code into Logical Groups:** Namespaces were used in older TypeScript code to organize code into logical groups. However, modules are now the preferred way to organize code, so namespaces are less common.

    ```typescript
    namespace MyNamespace {
        export interface MyInterface {
            value: string;
        }

        export class MyClass implements MyInterface {
            value: string;
            constructor(value: string) {
                this.value = value;
            }
        }
    }

    const myInstance = new MyNamespace.MyClass("Hello from namespace");
    console.log(myInstance.value); // Output: Hello from namespace
    ```
