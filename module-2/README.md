# Module 2: Working with Types

This module dives deeper into TypeScript's type system, covering how to define more complex types for objects, arrays, functions, and more.

## 2.1 Objects and Interfaces

*   **Defining Object Types using Interfaces:** Interfaces are a powerful way to define the shape of objects. They specify the names and types of properties an object should have.

    ```typescript
    interface Person {
      name: string;
      age: number;
      email: string;
    }

    const person1: Person = {
      name: "Alice",
      age: 30,
      email: "alice@example.com",
    };

    // const person2: Person = {  // Error: Missing 'email' property
    //   name: "Bob",
    //   age: 25,
    // };
    ```

*   **Optional Properties:** Use `?` to mark a property as optional.

    ```typescript
    interface Car {
      make: string;
      model: string;
      year: number;
      color?: string; // Optional property
    }

    const car1: Car = {
      make: "Toyota",
      model: "Camry",
      year: 2023,
    };

    const car2: Car = {
      make: "Honda",
      model: "Civic",
      year: 2022,
      color: "Red",
    };
    ```

*   **Readonly Properties:** Use `readonly` to prevent modification of a property after it's initialized.

    ```typescript
    interface Point {
      readonly x: number;
      readonly y: number;
    }

    const origin: Point = { x: 0, y: 0 };
    // origin.x = 10; // Error: Cannot assign to 'x' because it is a read-only property.
    ```

*   **Type Aliases:** Create a new name for a type. This can improve code readability, especially for complex types.

    ```typescript
    type Point2D = {
      x: number;
      y: number;
    };

    const p1: Point2D = { x: 10, y: 20 };
    ```

*   **Intersection Types (`&`):** Combine multiple types into one. The resulting type has all the properties of the combined types.

    ```typescript
    interface Colorful {
      color: string;
    }

    interface Circle {
      radius: number;
    }

    type ColorfulCircle = Colorful & Circle;

    const myCircle: ColorfulCircle = {
      color: "blue",
      radius: 5,
    };
    ```

*   **Union Types (`|`):** Define a type that can be one of several types.

    ```typescript
    type Result = string | number;

    let outcome: Result = "Success";
    outcome = 123;
    ```

## 2.2 Arrays and Tuples

*   **Type Annotations for Arrays:** Specify the type of elements in an array.

    ```typescript
    let numbers: number[] = [1, 2, 3, 4, 5];
    let names: string[] = ["Alice", "Bob", "Charlie"];
    let bools: boolean[] = [true, false, true];

    let mixed: (string | number)[] = [1, "two", 3, "four"]; // Union type for mixed arrays
    ```

*   **Tuples:** Define a fixed-length array with specific types for each element.

    ```typescript
    let point: [number, number] = [10, 20]; // x and y coordinates
    let user: [string, number, boolean] = ["John", 30, true]; // name, age, isActive
    ```

## 2.3 Enums

*   **Defining Enums:** Enums provide a way to define a set of named constants.

    ```typescript
    enum Status {
      Pending, // 0
      InProgress, // 1
      Completed, // 2
      Rejected, // 3
    }

    let jobStatus: Status = Status.InProgress;
    console.log(jobStatus); // Output: 1
    ```

*   **String Enums:** Assign string values to enum members.

    ```typescript
    enum Direction {
        Up = "UP",
        Down = "DOWN",
        Left = "LEFT",
        Right = "RIGHT",
    }
    let move: Direction = Direction.Up;
    console.log(move); // Output: UP
    ```

*   **Numeric Enums:** Assign numeric values (or let TypeScript auto-increment).

## 2.4 Functions

*   **Type Annotations for Function Parameters and Return Values:**

    ```typescript
    function add(a: number, b: number): number {
      return a + b;
    }

    function greet(name: string): void {
      console.log(`Hello, ${name}!`);
    }
    ```

*   **Optional Parameters:** Use `?` to make a parameter optional.

    ```typescript
    function greetOptional(name: string, greeting?: string): void {
      console.log(`${greeting || "Hello"}, ${name}!`);
    }

    greetOptional("Alice"); // Hello, Alice!
    greetOptional("Bob", "Good morning"); // Good morning, Bob!
    ```

*   **Default Parameters:** Provide default values for parameters.

    ```typescript
    function greetDefault(name: string, greeting: string = "Hello"): void {
      console.log(`${greeting}, ${name}!`);
    }

    greetDefault("Alice"); // Hello, Alice!
    greetDefault("Bob", "Good morning"); // Good morning, Bob!
    ```

*   **Function Overloading:** Define multiple function signatures with different parameter types.

    ```typescript
    function add(a: number, b: number): number;
    function add(a: string, b: string): string;
    function add(a: any, b: any): any {
        return a + b;
    }

    console.log(add(1, 2));     // Output: 3
    console.log(add("hello", " world")); // Output: hello world
    ```

*   **Arrow Functions and their Type Annotations:**

    ```typescript
    const multiply = (a: number, b: number): number => a * b;
    ```

## 2.5 Type Assertions

*   **Overriding Type Inference:** Use type assertions to tell the compiler the type of a value when it can't infer it correctly. Be cautious with type assertions as they can mask potential errors if used incorrectly.

    ```typescript
    let someValue: any = "this is a string";

    let strLength: number = (someValue as string).length; // Using 'as'
    let strLength2: number = (<string>someValue).length; // Using angle brackets (less common)
    ```
