---
kind: "study-reference"
title: "React"
collection: "Frontend"
topic: "Frontend"
imported: "2026-10-13"
source_files: ["INTERVIEW PREP NOTES/React.docx"]
tags: ["career/library"]
source_status: "source-reference"
---

# React

[[The Climb/Career Library/Career Library]]

**React.js Fundamentals:**

**App.jsx****:**

- **Purpose:** This file generally contains the main application component, often named App. It's where the primary structure of the application is defined, including the main layout, routes, and any global state or context providers.

- **Contents:** The App component usually includes child components, routes (if using a router like React Router), and other application-level logic.

**main.jsx**** (or ****index.jsx****):**

- **Purpose:** This file is typically the entry point for the React application. It's responsible for rendering the root component (often App) into the DOM. This is where you usually set up React rendering, attach the application to a specific DOM element, and include any global configurations or providers (like state management or theme providers).

- **Contents:** It imports React and ReactDOM, the App component, and mounts the App component to a DOM element.

**JSX**

JSX, which stands for JavaScript XML, is a syntax extension for JavaScript commonly used with React to describe what the UI should look like. It allows you to write HTML-like code within JavaScript, making it easier to create and visualize the structure of your UI components.

Here's a basic example of a React component written with JSX:

import React from 'react';

function Greeting(props) {

  return <h1>Hello, {props.name}!</h1>;

}

function App() {

  return (

    <div>

      <Greeting name="World" />

      <Greeting name="React" />

    </div>

  );

}

export default App;

**Compilation:**

Before the browser can understand JSX, it needs to be transformed into regular JavaScript. This transformation is usually handled by a build tool like Babel. For example, the JSX <h1>Hello, {props.name}!</h1> compiles to:

javascript

Copy code

React.createElement('h1', null, `Hello, ${props.name}!`)

**Props:**

- **Passing Data:**

- Props are passed from parent components to child components.

- They are read-only and cannot be modified by the child component.

**Immutable:**

- Props are immutable, meaning they cannot be changed directly by the component receiving them.

- If a component needs to modify its data, it typically uses a state instead of props.

     Let's say we have a Greeting component that receives a name prop and displays a personalized greeting:

import React from 'react';

function Greeting(props) {

  return <h1>Hello, {props.name}!</h1>;

}

export default Greeting;

In another component, we can use the Greeting component and pass a name prop to it:

import React from 'react';

import Greeting from './Greeting';

function App() {

  return <Greeting name="John" />;

}

export default App;

## Source provenance

- [Original DOCX](file:///D:/HDD%20F/downloads/CV/Previous%20Exp%20%2B%20Interview%20Prep/INTERVIEW%20PREP%20NOTES/React.docx) · INTERVIEW PREP NOTES/React.docx

Original files remain unchanged outside the vault. Imported code is a reference, not tested or certified.
