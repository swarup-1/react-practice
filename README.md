# Practice Questions

## What is Redux, how is it different from Context API? Why use Redux over Context API?
   - According to official documentation Redux is a javascript library for predictable and maintainable global state management, primarily used with React. It helps manage application state in a centralized store, making it easier to manage and manipulate application data. Redux follows the principles of a unidirectional data flow, which means data flows in one direction through your application.

   - On the other hand, The Context API is a feature in React that provides a way to pass data through the component tree without having to pass props down manually at every level.It is useful when you have data that needs to be accessible by many components at different nesting levels.

   There are some differences between Redux and the Context API:

   - Redux provides a centralized store for all of your application's state, making it easier to manage and debug Context API allows you to create multiple contexts because of that it is more decentralized approach.
   - Redux can offer better performance in large applications because of its centralized store and efficient update mechanisms. Context API, especially when used with useContext, can lead to unnecessary re-renders in some cases.
   - Redux offers powerful debugging tools and middleware like Redux DevTools, which can improve the developer experience. Context API doesn't come with built-in tools for debugging.
   - It is alwaya preferable to use Redux over the Context API as Redux is better suited for large-scale applications where complex state management is required. Its centralized approach and predictability make it easier to scale.
   - Redux can offer better performance optimizations compared to Context API especially for deeply nested components. 
   - Redux's strict unidirectional data flow and powerful debugging tools make it easier to trace the flow of data and debug issues in large applications.
   - if you're working on a small to medium-sized application or want simpler approach to state management, Context API might be sufficient. It's important to evaluate needs and complexity of application before deciding between Redux and Context API.


## How can you optimize a React app?
   - Optimizing a React app involves several strategies to enhance its performance and user experience.
   - by Code Splitting means Break down the application into smaller chunks and load them asynchronously. This reduces initial load time and improves performance.
   - Minimize the size of JavaScript bundles by removing unnecessary dependencies, using tree shaking means removeing the dead code during build process
   - Lazy Loading: Load components, routes, or data only when they are needed, instead of loading everything directly. to achieve React provides features like React.lazy() and Suspense for lazy loading components.
   - Use memoization techniques & hooks provided by React like React.memo(), useMemo & useCallback or external libraries prevent unnecessary re-renders of components and computations.
   - If we are using content-heavy applications then implement SSR to improve initial load times, enable better SEO, and provide a faster performance.
   - Cache data on client side using browser cache storage, session storage, local storage to reduce server requests


## What are keys in React?
   - Keys in React are special attributes used for unique identify elements in an list. it helps React to identify which items have changed, are added, or removed during re-rendering. Keys should be stable, unique, and typically come from the data itself. They help React in maintaining component state across re-renders and optimizing performance by minimizing unnecessary DOM manipulations which enhance overall application performance. for e.g if we have a data of users & for key we used user name but there is a possibility that same name is repeated in that case if we want to update/delete perticular user's info then it get applied for all similar users who have same key so that it is always preferable to use primary keys(unique) as key for rendering data
   

## Difference between throttling and debouncing?
   - Throttling and debouncing are techniques used in JavaScript to control function executions in response to frequent events like scrolling or typing.
   - Throttling ensures that a function is not executed more than once within a specified time interval. If the function is called multiple times within the interval, only the first call is executed & others are ignored.
   - Debouncing, delays the execution of a function after a certain amount of time has passed since the last invocation of the function. If the function is called multiple times within the debounce period, the previous invocations are canceled, and the function will only be executed once the debounce period ends without any further calls.


## What are Higher Order Components in React?
   - Higher Order Components (HOCs) in React are functions that take a component and return a new component.
   - HOC receives single or multiple components, enhance them with props, state & functionality & return a new component with those enhancements
   - it is used in code reusability They allow you to use common logic and behavior and apply it to multiple components of your application.
   - HOCs are commonly used for tasks such as data fetching, authentication, authorization, code splitting, and more.
   - HOCs are pure functions that do not modify the original component. Instead, they create and return a new component.
   - HOC names start with "with" to indicate their purpose, such as withData, withAuth, etc.


## What is lazy loading?
   - Lazy loading is a technique used in web development to stop loading the non-essential resources until they are actually needed. This helps improve the initial loading time and performance of web pages by prioritizing the loading of critical resources and deferring the loading of less important or bulky resources.
   - lazy loading is commonly used for Loading images only when they enter the viewport or when they are about to be displayed on the screen, rather than loading all images directly. Loading JavaScript code dynamically, particularly for components or libraries that are not immediately required on page load. Loading CSS stylesheets on demand
   - In react we use React.lazy() and Suspense to achieve lazy loading
   ```jsx
    import { useState, Suspense, lazy } from 'react';
    import Loading from './Loading.js';

    const NewLazyComponent = lazy(() => delayForDemo(import('./LazyComponent.js')));

    export default function MarkdownEditor() {
        const [showPreview, setShowPreview] = useState(false);
        const [input, setInput] = useState('Hello, **world**!');
        return (
            <>
            <textarea value={input} onChange={e => setInput(e.target.value)} />
            <label>
                <input type="checkbox" checked={showPreview} onChange={e => setShowPreview(e.target.checked)} />
                Show preview
            </label>
            <hr />
            {showPreview && (
                <Suspense fallback={<Loading />}>
                <h2>Preview</h2>
                <NewLazyComponent markdown={input} />
                </Suspense>
            )}
            </>
        );
    }

    // Add a fixed delay so you can see the loading state
    function delayForDemo(promise) {
        return new Promise(resolve => {
            setTimeout(resolve, 2000);
        }).then(() => promise);
    }
  ```

## How do you fetch a given API and render the data in the UI?
   - To fetch data from an API and render it in the UI in a React application, you typically use the fetch API, axios, or other similar libraries to make the HTTP request.
   ```jsx
   import React, { useState, useEffect } from 'react';

    const App = () => {
    const [data, setData] = useState(null);
    const [isLoading, setIsLoading] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
        const fetchData = async () => {
        try {
            const response = await fetch('https://api.example.com/data');
            if (!response.ok) {
            throw new Error('Failed to fetch data');
            }
            const jsonData = await response.json();
            setData(jsonData);
            setIsLoading(false);
        } catch (error) {
            setError(error.message);
            setIsLoading(false);
        }
        };

        fetchData();
    }, []);

    return (
        <div>
        <h1>API Data Example</h1>
        {isLoading && <div>Loading...</div>}
        {error && <div>Error: {error}</div>}
        {data && (
            <ul>
            {data.map(item => (
                <li key={item.id}>{item.name}</li>
            ))}
            </ul>
        )}
        </div>
    );
    };

    export default App;
  ```

## Discussion on projects.


## What is the virtual DOM and how does it work in React?
   - The virtual DOM (VDOM) is a concept used in React to improve performance by minimizing the number of direct manipulations to the actual DOM. It's a lightweight copy of the real DOM, maintained by React, that reflects the current state of the UI. When changes are made to the UI, React first updates the virtual DOM, then compares it with the previous version (reconciliation), and finally applies only the necessary changes to the real DOM.
   - React applies only the necessary changes to the real DOM to bring it in sync with the updated virtual DOM. This process is optimized to minimize DOM manipulations, resulting in better performance.
   - This makes React applications faster and more responsive, even when dealing with complex UIs and frequent updates.


## Explain the React component lifecycle.
   - The React component lifecycle refers to the series of phases or stages that a React component goes through from its creation to its removal from the DOM.
   - The lifecycle is divided into three main phases Mounting Phase, Updating Phase & Unmounting Phase
   - Mounting: In this phase, a component is initialized and inserted into the DOM. The lifecycle methods involved are constructor, render, componentDidMount.
   - Updating: This phase occurs when a component's state or props change. It involves re-rendering the component. Lifecycle methods include shouldComponentUpdate, render, componentDidUpdate.
   - Unmounting: This phase happens when a component is removed from the DOM. The componentWillUnmount method is invoked before the component is unmounted.


## What are controlled and uncontrolled components in React?
   - In React, controlled and uncontrolled components refer to two different approaches for handling form elements and managing their state.
   - Controlled Components: These components have their state controlled by React. They receive their current value and change event handlers as props. Any changes to the component's value are handled by updating the state, which triggers a re-render to reflect the new value. Controlled components provide control over the form elements' behavior and state.
   - Uncontrolled Components: These components allow the form elements to maintain their own state, independent of React's state management. They typically use refs to access the DOM directly and retrieve or modify the form element's values. Uncontrolled components are useful when integrating with non-React code or when you want to handle form state without managing it through React's state management system.


## How do you handle forms in React?
   - Handling forms in React typically involves using controlled components, where form elements such as inputs, selects, and textareas are controlled by React state. The general approach is Initialize state variables to hold the values of form inputs.
   - Implement form validation like required & input type etc
   - Create event handler functions to update the state when form inputs change. like onChange
   - Bind form elements to state by setting their value attributes to the corresponding state variables and their onChange attributes to the event handler functions.
   - Handle form submission by creating a submit event handler function using onSubmit attribute.


## Explain the concept of "lifting state up" in React.
   - "Lifting state up" means in React where you move the state of a component upwards in the component hierarchy to share it with multiple child components. This pattern promotes the idea of a single source of truth for state management.
   - Firstly we determine if multiple components need access to the same state data.
   - If multiple components require the same state, lift the state up to the closest common ancestor.
   - Pass down the state data from the parent component to the child components as props.
   - Handle state updates in the parent component.


## What are React hooks and why are they useful?
   - In React Functional Components the hooks are used these are the functions to use state & lifecycle features that are available previously for class components only.
   - Hooks provide a way to use stateful logic and side effects in functional components without the need for class syntax or lifecycle methods. They allow developers to write more readable and reusable code.
   - Some commonly used React hooks include:
   useState: Allows functional components to manage local state.
   useEffect: Allows functional components to perform side effects (e.g., data fetching, DOM manipulation) in response to component lifecycle events (e.g., mounting, updating, unmounting).
   useContext: Allows functional components to consume context provided by a Context.Provider component.
   useReducer: Provides an alternative to useState for managing more complex state logic using a reducer function.
   useRef: Allows functional components to create mutable references to DOM elements or other values that persist across renders.


## How do you manage side effects in React applications?
   - In React applications, side effects such as data fetching, subscriptions, or DOM manipulations are managed using the useEffect hook. useEffect allows you to perform side effects in functional components in response to component lifecycle events like mounting, updating, and unmounting.
   - If you pass an empty dependency array ([]) as the second argument to useEffect, the effect will run only once after the component mounts. Like an Mounting phase
   - If you pass an array of dependencies to useEffect, the effect will run after the component mounts and whenever any of the specified dependencies change. Like an Update phase
   - If the effect returns a cleanup function, React will run it when the component unmounts. This allows you to perform cleanup operations such as unsubscribing from event listeners or canceling network requests. 


## What is React Router and how do you implement it?
   - React Router is a popular library for handling routing in React applications. It allows you to define and manage navigation between different components or pages in your application, enabling the creation of single-page applications (SPAs) with dynamic, client-side routing.
   - To implement React Router in your React application we need to install from package managers.
   - To setup firstly we need to import required components from react-router-dom
   - Wrap the application in a `<BrowserRouter>` component and define routes using the `<Routes>` and `<Route>`components.
   - Use the `<Link>` component for navigation within your application instead of using anchor tags (<a>), which reload the page.
   - You can navigate programmatically using the useNavigate() hook:


## Explain the concept of prop drilling and how to avoid it.
   - Prop drilling is a term used to describe the process of passing data from a parent component down to deeply nested child components through intermediate components. This often results in components receiving props that they do not directly need, only to pass them further down the component tree. This can make the code harder to manage, understand, and maintain.
   - To avoid prop drilling, you can use several techniques such as Context API, State Management Libraries.
   - The React Context API allows you to create a context and pass data to any component in the tree without passing props explicitly through every level.
   - Libraries like Redux, MobX can be used to manage state globally, making it accessible to any component in the application without the need for prop drilling.
   - By using these techniques, you can avoid the issue of prop drilling, making your codebase cleaner, more maintainable, and easier to understand.


## What are fragments in React and why are they used?
   - Fragments in React allow you to group a list of children elements without adding extra nodes to the DOM. They are particularly useful when you want to return multiple elements from a component without wrapping them in a parent element like a `<div>`, which can lead to unnecessary nesting and can complicate styling and layout.
   - Using the short syntax, which is an empty tag `<>`, is a concise way to use fragments. This syntax is not supported if you need to use keys or attributes.
   - Using the `<React.Fragment key={anything}>` component is more verbose but allows you to use keys and other attributes if needed.
   ```jsx
    const ExampleComponent = () => {
        return (
            <>
            <h1>Title</h1>
            <p>Description</p>
            </>
        );
    };
    // OR
    const ExampleComponent = () => {
        return (
            <React.Fragment>
            <h1>Title</h1>
            <p>Description</p>
            </React.Fragment>
        );
    };
  ```
   - By using fragments, you can keep your markup clean and avoid unnecessary parent elements, making your application more efficient and your code easier to maintain.


## How do you handle error boundaries in React?
   - In React, error boundaries are components that catch JavaScript errors anywhere in their child component tree, log those errors, and display a fallback UI instead of crashing the whole component tree. Error boundaries are typically implemented in class components, but with the introduction of hooks, they can also be managed in functional components using custom hooks.
   ```jsx
   import React, { useState, useEffect } from 'react';

    const useErrorBoundary = () => {
    const [hasError, setHasError] = useState(false);

    useEffect(() => {
        const errorHandler = (error) => {
        setHasError(true);
        console.error(error);
        };

        window.addEventListener('error', errorHandler);
        window.addEventListener('unhandledrejection', errorHandler);

        return () => {
        window.removeEventListener('error', errorHandler);
        window.removeEventListener('unhandledrejection', errorHandler);
        };
    }, []);

    return hasError;
    };

    const ErrorBoundary = ({ children }) => {
    const hasError = useErrorBoundary();

    if (hasError) {
        return <h1>Something went wrong.</h1>;
    }

    return children;
    };

    export default ErrorBoundary;
  ```
   

## What is the difference between state and props in React?
   - In React, both state and props are plain JavaScript objects and used to manage the data of a component, but they are used in different ways and have different characteristics.
   - The state entity is managed by the component itself and can be updated using the setter(setState() for class components) function. Unlike props, state can be modified by the component and is used to manage the internal state of the component. Moreover, changes in the state trigger a re-render of the component and its children. The components cannot become reusable with the usage of state alone.
   - On the otherhand, props (short for "properties") are passed to a component by its parent component and are read-only, meaning that they cannot be modified by the own component itself. Also, props can be used to configure the behavior of a component and to pass data between components. The components become reusable with the usage of props.


## How do you implement server-side rendering (SSR) in a React application?
   - Server-side rendering (SSR) in a React application involves rendering React components on the server and sending the generated HTML to the client. This can improve performance and SEO, especially for initial page loads. One of the most popular ways to implement SSR in React is by using a framework like Next.js, which provides built-in support for SSR.
   - Next.js is a React framework that provides an easy way to implement SSR along with other features like static site generation (SSG), API routes, and more.


## Explain the difference between functional and class components in React.
   - In React, functional components and class components are two primary ways to define a component's behavior and structure.
   - Functional Components: Defined as JavaScript functions. They accept props as arguments and return JSX.
   - Class Components: Defined as ES6 classes that extend React.Component. They can have a constructor and lifecycle methods like render(), componentDidMount(), etc.
   - With the introduction of hooks, functional components can now use state and other React features using hooks like useState, useEffect, etc.
   - Class components Can have state managed using this.state and this.setState()
   - With hooks, functional components can use lifecycle methods using hooks like useEffect, useLayoutEffect, etc.
   - Class components have lifecycle methods like componentDidMount(), componentDidUpdate(), componentWillUnmount(), etc.
   - functional components are becoming the preferred way to define React components due to their simplicity, readability, and the introduction of hooks, which allow them to have state and lifecycle behaviors similar to class components. However, class components still have their place, especially in legacy codebases and for certain use cases that require specific lifecycle methods or class features.


## How do you optimize a React application's performance using code splitting?
   - In a React application, optimizing performance is crucial for providing a smooth user experience. One technique to achieve this is code splitting, which involves breaking down your application's code into smaller, more manageable chunks and only loading the necessary code when it's needed.
   - Determine which parts of your application can benefit from code splitting. Typically, large libraries, components, or routes that are not immediately needed on the initial page load are good candidates for code splitting.
   - In React, you can use the React.lazy() function along with the Suspense component to lazily load components.
   - Implement code splitting based on routes in your application. Only load the JavaScript bundles required for the current route, and lazy load components associated with other routes to reduce the initial bundle size.
   - By effectively implementing code splitting in your React application, you can reduce the initial bundle size, improve load times, and provide a faster and more responsive user experience, especially for users on slower network connections or devices.
   

## What are portals in React and when would you use them?
   - Portals in React provide a way to render children into a DOM node that exists outside the hierarchy of the parent component. This can be useful for various scenarios when implementing modals, tooltips, or popovers.
   - Portals are often used for rendering modals or dialogs that should appear on top of other content, not constrained by the parent component's styling or z-index.
   - Similar to modals, tooltips and popovers need to appear above other content and should not be affected by the overflow and positioning of parent components.
   - Overlays, dropdown menus, and context menus can also benefit from portals to ensure they are positioned correctly and are not affected by the parent component's overflow settings.
   - Portals are a powerful feature in React that enable you to render components outside their parent hierarchy, providing flexibility for creating components like modals, tooltips, and overlays. They help maintain a clean and modular codebase while ensuring that UI components are displayed correctly and without constraints from parent components.


## How do you handle asynchronous operations in React?
   - Handling asynchronous operations in React is a common requirement, especially when dealing with data fetching, API calls, and other side effects.
   - There are multiple ways to handle asynchronous operations
   - One of the most common patterns is to use the useEffect hook combined with async/await for asynchronous operations. Since the useEffect function itself cannot be async, you define an async function inside the effect and call it.
   - Alternatively, you can handle promises directly inside useEffect.
   - For better reusability and separation of concerns, you can create a custom hook to handle asynchronous operations.
   - For handling asynchronous events, such as form submissions or button clicks, you can use async functions directly.
   - By following these patterns and best practices, you can efficiently manage asynchronous operations in your React applications, ensuring smooth user experiences and maintainable code.


## What is the significance of the `useEffect` hook and how is it used?
   - The useEffect hook is one of the most powerful and commonly used hooks in React. It allows you to perform side effects in your functional components. Side effects are operations that can affect the state or behavior of your application.Examples include fetching data, directly manipulating the DOM etc
   - In functional components of react useEffect hook used instead of lifecycle methods from class components
   - It's commonly used for data fetching and can be configured to run when the component mounts or when certain state variables change.
   - You can use useEffect to set up subscriptions or event listeners, and clean them up when the component unmounts or when dependencies change.
   - helps in optimizing performance by avoiding unnecessary re-runs of the effect.
   ```jsx
   const MyComponent = () => {
   useEffect(() => {
      // Code to run on component mount (and on updates, if dependencies are not specified)
      return () => {
         // Cleanup code to run on component unmount
      };
   }, [/* dependencies*/]);
   ```


## How do you create a custom hook in React?
   - Creating a custom hook in React allows you to extract and reuse logic across multiple components. Custom hooks are regular JavaScript functions whose names start with "use" and can call other hooks. 
   - Identify logic that is used by multiple components and can be changed into reusable function.
   - Define a function that cover the logic and can be reused. This function should start with the word "use".
   - You can use built-in hooks (like useState, useEffect, etc.)
   - Take required props & Return the necessary state and functions from the custom hook so that consuming components can use them.
   - Benifits: Custom hooks allow you to reuse logic across multiple components, reducing code duplication. Extracting complex logic into custom hooks makes your components cleaner and easier to read.
   Easier to test and maintain.
   ```jsx
      import { useState, useEffect } from 'react';

      const useFetch = (url) => {
      const [data, setData] = useState(null);
      const [loading, setLoading] = useState(true);
      const [error, setError] = useState(null);

      useEffect(() => {
         const fetchData = async () => {
            setLoading(true);
            try {
               const response = await fetch(url);
               const result = await response.json();
               setData(result);
               setError(null);
            } catch (error) {
               setError(error);
               setData(null);
            }
            setLoading(false);
         };

         fetchData();
      }, [url]);

      return { data, loading, error };
      };

      export default useFetch;

      // Used as:
      const { data, loading, error } = useFetch('https://api.example.com/data');
      if (loading) return <p>Loading...</p>;
      if (error) return <p>Error: {error.message}</p>;
  ```


## Explain the context API and its use cases.
   - The Context API in React is a feature that allows you to manage global state or data that can be shared across the entire component tree without the need to pass props down manually through each nested component. This can be particularly useful for managing state that needs to be accessible by many components at different levels of the application.
   - Use React.createContext() to create a Context object.
   - The Provider component is used to wrap the part of your application
   - Use the useContext hook in functional components
   - It is widely used in Theme Management, User Authentication, Language Localization, Global State Management.
   - Share theme information (e.g., light/dark mode) across the application to ensure consistent styling.
   - Manage user authentication state (e.g., user login status, user details) and share it across different parts of the application without prop drilling.
   - Provide localized text and manage the current language or locale for internationalization purposes.
   - Manage global state that needs to be accessed by multiple components, such as application settings, notifications, or user preferences.
   ```jsx
      // ThemeContext.js
      import React, { createContext, useState } from 'react';
      export const ThemeContext = createContext();

      export const ThemeProvider = ({ children }) => {
      const [theme, setTheme] = useState('light');

         return (
            <ThemeContext.Provider value={{ theme, setTheme }}>
               {children}
            </ThemeContext.Provider>
         );
      };
      // App.js
      const App = () => {
         return (
            <ThemeProvider>
               <Header />
               <Content />
            </ThemeProvider>
         );
      };
      // Header.jsx
      const Header = () => {
      const { theme, setTheme } = useContext(ThemeContext);

      return (
               <h1>Theme is {theme}</h1>
               <button onClick={() => setTheme(theme === 'light' ? 'dark' : 'light')}>Toggle Theme</button>
         );
      };
  ```


## What are the best practices for structuring a React application?
   - Structuring a React application is essential for maintainability, scalability, and code organization. 
   - Organize the application into reusable components that encapsulate logic and UI elements.
   - Break down the UI into smaller, manageable pieces, making it easier to understand, test, and maintain.
   - Arrange files and folders in a logical structure that reflects the application's features and functionality.
   - Use a modular folder structure, grouping related components, styles, and assets together.
   - Separate concerns by keeping logic, presentation, and styling concerns separate within components.
   - Choose an appropriate state management solution based on the complexity and scale of your application (e.g., React Context, Redux) Centralize state management to avoid prop drilling and maintain a single source of truth for application state.
   - Use a routing library (e.g., React Router) for managing navigation and routing within the application.
   - Split large chunks of code into smaller, dynamically loaded chunks using techniques like React.lazy() for lazy loading components.
   - Implement error boundaries to handle errors and prevent them from crashing the entire application.
   - Write unit tests for components, reducers, and utility functions using testing libraries like Jest and React Testing Library.
   - Choose a styling approach that fits your project's requirements (e.g., CSS Modules, Styled Components, CSS-in-JS).
   - Document codebase architecture, component APIs, and project conventions to facilitate collaboration and onboarding of new team members.
   - Optimize rendering performance, reduce unnecessary re-renders, and minimize the use of expensive operations in components.


## How do you handle authentication and authorization in a React application?
   - Handling authentication and authorization in a React application is crucial for ensuring that users can securely access resources and perform actions within the application.
   - Authentication is the process of verifying the identity of a user or system. It involves validating the credentials provided by a user to prove their identity.
   - Implement user authentication using techniques like username/password authentication, social login (OAuth), or token-based authentication (JWT).
   - Store authentication state in the application, indicating whether a user is authenticated or not. This state can be stored in React context, Redux state, or local component state.
   - Implement backend APIs for handling authentication requests, such as verifying user credentials, generating access tokens, and refreshing tokens
   - Store access tokens securely, such as in browser cookies with the `HttpOnly` and `Secure` flags
   - Authorization, also known as access control, is the process of determining what actions a user or system is allowed to perform on a resource or within an application. It involves enforcing rules and policies to restrict access to authorized users only. 
   - Define roles and permissions for different user types in the application. Determine what actions each role is allowed to perform.
   - Use route guards or middleware to protect routes that require authentication or specific user roles/permissions. Redirect unauthenticated users to the login page or show an appropriate error message.
   - Implement backend APIs for handling authorization requests, such as validating access tokens, checking user roles/permissions, and enforcing access control rules.
   - Conditionally render UI components based on the user's permissions to hide or show certain features or functionalities. 


## What is the `useCallback` hook and when would you use it?
   - The useCallback hook in React is used to memoize callback functions so that they are only recreated when their dependencies change. It memoizes the callback function so that the same function instance is returned on subsequent renders unless the dependencies have changed.
   - Use useCallback when passing callback functions as props to child components to prevent unnecessary re-renders. By memoizing the callback function, you ensure that the same function instance is passed down to the child component unless the dependencies change.
   - If a callback function is created inside a component's render function, it will be recreated on every render, even if the component's state or props haven't changed. Use useCallback to memoize the callback function and optimize performance by avoiding unnecessary recreations.
   - hen a callback function depends on certain values from the component's state or props, you can use useCallback to prevent unnecessary re-renders
   

## What is the `useMemo` hook and when would you use it?
   - The `useMemo()` hook in React is used for memoizing expensive calculations so that they are only re-computed when their dependencies change. It memoizes the result of a function so that the function is not re-executed unnecessarily on every render.
   - Use `useMemo()` when we have expensive calculations or computations in our component that do not depend on every render cycle. By memoizing the result of the computation, we can avoid re-computing it on every render.
   - If a computation within a component depends on certain inputs (dependencies) that don't change frequently, we can use `useMemo()` to memoize the result.
   - Use `useMemo()` to optimize the performance of your components by preventing unnecessary re-renders.
   - `useMemo()` can also be used to memoize components or values that are expensive to create.