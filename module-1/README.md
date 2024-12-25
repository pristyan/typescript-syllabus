# Module 1: Introduction to TypeScript

## 1.1 What is TypeScript?

*   **TypeScript as a Superset of JavaScript:**
    *   TypeScript extends JavaScript by adding static typing. This means you can specify the types of variables, function parameters, and return values.
    *   Any valid JavaScript code is also valid TypeScript code. This allows you to gradually introduce TypeScript into existing JavaScript projects.
*   **Benefits of Using TypeScript:**
    *   **Early Error Detection:** TypeScript catches type errors during development (compile time), preventing runtime errors and making debugging easier.
    *   **Improved Code Maintainability:** Types act as documentation, making it easier to understand and refactor code, especially in large projects.
    *   **Enhanced Tooling:** IDEs provide better autocompletion, code navigation, and refactoring support with TypeScript.
    *   **Better Collaboration:** Type definitions make it easier for teams to collaborate on code, as everyone has a clear understanding of the data structures.
*   **Setting up Your Development Environment:**
    *   **Node.js and npm/yarn:** Make sure you have Node.js and npm (Node Package Manager) or yarn installed. You can download them from [https://nodejs.org/](https://nodejs.org/).
    *   **Installing TypeScript:** Install TypeScript globally using npm or yarn:

        ```bash
        npm install -g typescript  # Using npm
        yarn global add typescript # Using yarn
        ```

    *   **TypeScript Compiler (tsc):** The `tsc` command is the TypeScript compiler. It's used to compile `.ts` files into `.js` files.

## 1.2 Basic Types:

*   **`number`:** Represents numeric values (integers and floating-point numbers).

    ```typescript
    let age: number = 30;
    let price: number = 99.99;
    ```

*   **`string`:** Represents text values.

    ```typescript
    let name: string = "John Doe";
    let message: string = 'Hello, world!';
    ```

*   **`boolean`:** Represents true or false values.

    ```typescript
    let isDone: boolean = false;
    let isValid: boolean = true;
    ```

*   **`any`:** Represents any type. Using `any` disables type checking for that variable. Avoid using `any` as much as possible.

    ```typescript
    let anything: any = "a string";
    anything = 123;
    anything = true; // No error
    ```

*   **`unknown`:** Represents an unknown type. Unlike `any`, you need to perform type checking or assertions before using a value of type `unknown`.

    ```typescript
    let value: unknown = "hello";
    if (typeof value === "string") {
      console.log(value.toUpperCase()); // Now it's safe
    }
    ```

*   **`void`:** Represents the absence of a value, typically used for function return types.

    ```typescript
    function greet(): void {
      console.log("Hello!");
    }
    ```

*   **`null` and `undefined`:** Represent the absence of a value. In strict mode (`strictNullChecks`), you need to explicitly allow `null` or `undefined` in your types.

    ```typescript
    let nullableValue: string | null = null;
    let undefinedValue: number | undefined = undefined;
    ```

*   **Type Inference:** TypeScript can often infer the type of a variable based on its initial value.

    ```typescript
    let count = 10; // TypeScript infers 'count' as 'number'
    let greeting = "Hello"; // TypeScript infers 'greeting' as 'string'
    ```

*   **Type Annotations:** Explicitly specifying the type of a variable.

    ```typescript
    let age: number;
    age = 30;
    ```

## 1.3 Basic Syntax and Operators:

*   **Variables (`let`, `const`):**
    *   `let`: Used for variables that can be reassigned.
    *   `const`: Used for constants (values that cannot be reassigned).

    ```typescript
    let counter = 0;
    counter++;

    const PI = 3.14159;
    // PI = 3.14; // Error: Cannot reassign constant
    ```

*   **Operators:**
    *   Arithmetic operators: `+`, `-`, `*`, `/`, `%`, `++`, `--`
    *   Comparison operators: `==`, `===`, `!=`, `!==`, `>`, `<`, `>=`, `<=`
    *   Logical operators: `&&`, `||`, `!`

*   **Control Flow:**
    *   `if/else` statements:

        ```typescript
        let x = 10;
        if (x > 5) {
          console.log("x is greater than 5");
        } else {
          console.log("x is not greater than 5");
        }
        ```

    *   `switch` statements:

        ```typescript
        let day = "Monday";
        switch (day) {
          case "Monday":
            console.log("It's Monday!");
            break;
          // ... other cases
          default:
            console.log("It's another day.");
        }
        ```

    *   `for` loops:

        ```typescript
        for (let i = 0; i < 10; i++) {
          console.log(i);
        }
        ```

    *   `while` loops:

        ```typescript
        let i = 0;
        while (i < 5) {
          console.log(i);
          i++;
        }
        ```

## 1.4 Compiling TypeScript:

*   **`tsc` Command:** The basic command to compile a TypeScript file is:

    ```bash
    tsc filename.ts
    ```

    This will generate a `filename.js` file in the same directory.

*   **`tsconfig.json` Configuration File:** A `tsconfig.json` file is used to configure the TypeScript compiler. It contains options that control how the code is compiled.

    ```json
    {
      "compilerOptions": {
        "target": "es2020", // Target JavaScript version
        "module": "commonjs", // Module system
        "strict": true,      // Enable strict type checking
        "outDir": "./dist" // Output directory for compiled JavaScript
      }
    }
    ```

    With a `tsconfig.json` file, you can compile all TypeScript files in a project by simply running:

    ```bash
    tsc
    ```

## 1.5 Basic Debugging:

*   **Setting up Debugging in VS Code:**
    *   Install the "Debugger for Chrome" (or your preferred browser's debugger) extension in VS Code.
    *   Create a `launch.json` file in your project's `.vscode` folder.
    *   Configure the `launch.json` file to launch your application in debug mode.
