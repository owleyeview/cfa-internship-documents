# React
## What is it?
### A frontend Javascript library (framework?)
- designed for making building the frontend easier
- standardized format
- gives your project an easier to understand structure
- open-source project created by Facebook

## Why use it?
1. Declarative UI: With React, you describe the UI in a declarative manner, meaning you tell it what you want (e.g., a button, a list) without worrying about how the browser will render it. The reconciliation algorithm of React takes care of efficient updates.

2. State Management: React components can have local states. Whenever the state changes, React efficiently updates the part of the UI that depends on that state. This is contrasted with traditional JavaScript where you'd have to manually find the DOM element and update it.

3. Lifecycle Methods: React components have lifecycle methods that allow you to run code at specific times in a component's life, such as when it first mounts to the DOM or before it updates.

4. JSX: JSX lets you write HTML-like syntax in your JavaScript code which gets transcompiled to regular JavaScript. It makes component code more readable and intuitive.

Without React, achieving a dynamic, state-driven UI typically involves manually updating the DOM, which can be error-prone, less efficient, and harder to maintain.
- React isn't always necessary for simple projects

## How to use it?
Create React App will scaffold an app for you
From terminal:
- `npx create-react-app [my-app]`
- `cd [my-app]`
- `npm start` // opens the app on localhost:3000

## What is in a React app?
### README.md
- explanations and helpful commands related to your React app
### package.json
- dependencies and scripts
### app.js
- this is where you make your app

## Components
### Overview
React introduces the concept of UI components.  These are encapsulations of a piece of the user interface.  Each component can have its own internal state, lifecycle methods, and is designed to be reusable.
React has Class components and Functional components
- Class components can define a state
- Functional components are stateless
	- Hooks are used to deal with state 
Each React component can only return one element at the top level.  If you want to return multiple elements at the top level of a component, you can wrap them in another div or fragment that becomes the top level parent.
Common Component Structure:
- hooks at the top
- helper functions or data parsing code
- return containing the .jsx 

#### Props
Props allow you to pass information down to custom components
### React Hooks

React hooks are...
React hooks cannot be run conditionally and good practice is to put them at the top of your file.
#### useEffect()
- the `useEffect()` hook allows you to perform side effects (like data fetching, socket connections, manual DOM manipulations) in functional components.
- `useEffect()` takes two arguments: a function that contains the code to run and a dependency array.
- if the dependency array is empty, the effect runs once after the component mounts
- if the dependency array is not included in the `useEffect()` declaration, the effect will run after every render
- if the dependency array contains some prop or state, the effect only runs when that prop or state changes
#### useState()
- the `useState()` function returns an array with two items.  The first item is the current state value, and the second is a function to update the state.  
- every time you call the update function with a value, React knows to re-render the component with the updated state value.  

## Helpful Resources 
Web Dev Simplified- Learn React [video](https://youtu.be/Rh3tobg7hEo)
- Great intro to React when you already have good basic JavaScript knowledge