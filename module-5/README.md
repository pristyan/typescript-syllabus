# Module 5: TypeScript with React

This module focuses on using TypeScript with the React library. It covers how to type React components, hooks, events, and the Context API.

## 5.1 Setting up a React Project with TypeScript

*   **Using Create React App with the TypeScript Template:** The easiest way to start a new React project with TypeScript is to use Create React App with the `--template typescript` flag:

    ```bash
    npx create-react-app my-react-ts-app --template typescript
    cd my-react-ts-app
    ```

    This will create a new React project with all the necessary TypeScript configurations.

*   **Manual Setup:** If you're adding TypeScript to an existing React project, you'll need to install the necessary packages and configure the TypeScript compiler:

    ```bash
    npm install --save typescript @types/react @types/react-dom @types/node
    # or
    yarn add typescript @types/react @types/react-dom @types/node
    ```

    Then, create a `tsconfig.json` file in your project root. A basic `tsconfig.json` for a React project might look like this:

    ```json
    {
      "compilerOptions": {
        "target": "es5",
        "lib": [
          "dom",
          "dom.iterable",
          "esnext"
        ],
        "allowJs": true,
        "skipLibCheck": true,
        "esModuleInterop": true,
        "allowSyntheticDefaultImports": true,
        "strict": true,
        "forceConsistentCasingInFileNames": true,
        "module": "esnext",
        "moduleResolution": "node",
        "resolveJsonModule": true,
        "isolatedModules": true,
        "noEmit": true,
        "jsx": "react-jsx"
      },
      "include": [
        "src"
      ]
    }
    ```

## 5.2 Typing React Components

*   **Functional Components with Type Annotations for Props:**

    ```typescript jsx
    import React from 'react';

    interface GreetingProps {
      name: string;
      enthusiasmLevel?: number; // Optional prop
    }

    const Greeting: React.FC<GreetingProps> = ({ name, enthusiasmLevel = 1 }) => {
      return (
        <div>
          <h1>Hello, {name}{"!".repeat(enthusiasmLevel)}</h1>
        </div>
      );
    };

    const App = () => {
        return (
            <div>
                <Greeting name="Alice" enthusiasmLevel={3}/>
                <Greeting name="Bob" />
            </div>
        )
    }

    export default App;
    ```

*   **Class Components with Type Annotations for Props, State, and Methods:**

    ```typescript jsx
    import React from 'react';

    interface CounterProps {
      initialCount: number;
    }

    interface CounterState {
      count: number;
    }

    class Counter extends React.Component<CounterProps, CounterState> {
      constructor(props: CounterProps) {
        super(props);
        this.state = { count: props.initialCount };
      }

      increment = () => {
        this.setState(prevState => ({ count: prevState.count + 1 }));
      };

      render() {
        return (
          <div>
            <p>Count: {this.state.count}</p>
            <button onClick={this.increment}>Increment</button>
          </div>
        );
      }
    }

    export default Counter;
    ```

## 5.3 Typing React Hooks

*   **`useState`:**

    ```typescript jsx
    import React, { useState } from 'react';

    const MyComponent = () => {
      const [count, setCount] = useState<number>(0); // Type is number
      const [name, setName] = useState<string>(""); // Type is string
      const [items, setItems] = useState<string[]>([]); // Type is string array
      const [user, setUser] = useState<{name: string, age: number} | null>(null); // Type is object or null

      return (
        <div>
          <p>Count: {count}</p>
          <button onClick={() => setCount(count + 1)}>Increment</button>
        </div>
      );
    };
    ```

*   **`useEffect`:**

    ```typescript jsx
    import React, { useState, useEffect } from 'react';

    const MyComponent = () => {
      const [data, setData] = useState<string | null>(null);

      useEffect(() => {
        const fetchData = async () => {
          const response = await fetch('[https://api.example.com/data](https://api.example.com/data)');
          const result: string = await response.text(); // Type assertion if needed
          setData(result);
        };

        fetchData();
      }, []); // Empty dependency array for componentDidMount behavior

      return <div>{data}</div>;
    };
    ```

*   **`useContext`:** Covered in the Context API section below.

*   **`useReducer`:**

    ```typescript jsx
    import React, { useReducer } from 'react';

    interface State {
      count: number;
    }

    type Action = { type: 'increment' } | { type: 'decrement' };

    const reducer = (state: State, action: Action): State => {
      switch (action.type) {
        case 'increment':
          return { count: state.count + 1 };
        case 'decrement':
          return { count: state.count - 1 };
        default:
          return state;
      }
    };

    const MyComponent = () => {
      const [state, dispatch] = useReducer(reducer, { count: 0 });

      return (
        <div>
          Count: {state.count}
          <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
        </div>
      );
    };
    ```

*   **`useRef`:**

    ```typescript jsx
    import React, { useRef, useEffect } from 'react';

    const MyComponent = () => {
      const inputRef = useRef<HTMLInputElement>(null);

      useEffect(() => {
        if (inputRef.current) {
          inputRef.current.focus();
        }
      }, []);

      return <input type="text" ref={inputRef} />;
    };
    ```

## 5.4 Working with Events and Event Handlers

*   **Typing Event Handlers Correctly:**

    ```typescript jsx
    import React from 'react';

    const MyComponent = () => {
      const handleClick = (event: React.MouseEvent<HTMLButtonElement>) => {
        console.log('Button clicked!', event.currentTarget);
      };

      const handleChange = (event: React.ChangeEvent<HTMLInputElement>) => {
        console.log('Input changed:', event.target.value);
      };

      return (
        <div>
          <button onClick={handleClick}>Click me</button>
          <input type="text" onChange={handleChange} />
        </div>
      );
    };
    ```

## 5.5 Typing Context API

*   **Creating Type-Safe Context:**

    ```typescript jsx
    import React, { createContext, useContext } from 'react';

    interface Theme {
      primaryColor: string;
      secondaryColor: string;
    }

    const defaultTheme: Theme = {
      primaryColor: '#007bff',
      secondaryColor: '#6c757d',
    };

    const ThemeContext = createContext<Theme>(defaultTheme);

    const ThemeProvider: React.FC<{ children: React.ReactNode }> = ({ children }) => {
      const [theme, setTheme] = React.useState<Theme>(defaultTheme);

      return (
        <ThemeContext.Provider value={{ theme, setTheme }}>
          {children}
        </ThemeContext.Provider>
      );
    };

    const MyComponent = () => {
      const { theme } = useContext(ThemeContext);

      return (
        <div style={{ backgroundColor: theme.primaryColor, color: 'white', padding: '10px' }}>
          This component uses the theme context.
        </div>
      );
    };

    const App = () => {
        return (
            <ThemeProvider>
                <MyComponent />
            </ThemeProvider>
        )
    }

    export default App;
    ```

## 5.6 Working with Third-Party Libraries

*   **Using Type Definitions for Third-Party Libraries (`@types/*`):** Most popular JavaScript libraries have corresponding type definitions packages on npm under the `@types` scope. Install them using:

    ```bash
    npm install --save-dev @types/<library-name>
    # or
    yarn add -D @types/<library-name>
    ```

    For example, for the `lodash`
