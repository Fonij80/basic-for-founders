# Beginning ReactJS Foundations

- ReactJS released by facebook in 2013, front-end UI lib for web app
- React Native in 2015, UI lib for mobile app

- Node.js is needed to run JS on web servers

- Common tasks in development by Node.js:

1. **Minification**:
   process of removing not necessary codes (spaces, line breaks, comments) for the program to run
   Minification makes scripts, web pages, and stylesheets more efficient and faster.

2. **Transpiling**:
   process of converting programming code from one version of a programming language into another version, necessary in web development because not all web browsers support the same set of new JS features, but they do all support some
   core subset of JS features. By using a JS transpiler, programmers can write
   code using the latest version of JS and then the transpiled code can be run in any web browser.

3. **Module bundling**:
   A typical website can make use of hundreds of individual JS programs. If a web browser had to download each of these different programs individually, it
   would significantly slow down web pages due to the overhead involved with requesting files from web servers. The main job of a module bundler is to combine/bundle the JS and other code involved in a web app to make serving the app faster. Because a bundler has to do work to all of the files in a program, it also is a good
   central place for tasks like minification and transpiling to take place, through the use of
   plugins.

[Module bundling](../../assets/module_bundling.png)

4. **Package management**:
   help managing all the JS programs (packages) needed in your app

5. **CSS preprocessor**:
   A CSS preprocessor (like SASS or LESS) allows you to write style sheets using a superset of CSS (such as SCSS) that supports the programmatic features that CSS lacks (variables, mathematic operations, functions, scope, and nesting).
   A CSS preprocessor produces standard CSS from code written using an alternative syntax.

6. **Testing frameworks**

7. **Build automation**:
   process of writing a program or script that runs all of the
   different tools for you in the right order to quickly and reliably optimize, compile, test, and
   deploy applications.

- when you install Node.js, npm will also be installed for package management.

- upgrading npm:

```bash
sudo npm install -g npm
```

- create **package.json** to track dependencies:

```bash
npm init -y
```

- Node.js learning resource:

```bash
npm install learnyounode

or

sudo npm install learnyounode -g

learnyounode (run the package)
```

- In DevTools, what you’re changing is your web browser’s in-­memory representation of the web page. If you refresh the page, it will be re-­downloaded and will appear as it did when you first loaded it.

- DOM (Document Object Model): JS API for web pages

- The production version of React uses minified component names, and most of the debugging functionality is removed in order to increase performance and decrease the size of the download required for the browser to run React.

- The React components you can inspect through the React Developer Tools eventually produce the DOM nodes (which represent HTML and styles) that you can browse using the browser’s element inspector.

- The Profiler gives you information about the performance of your React application. Profiling is disabled in the production version of React, so this tab won’t do much when you view a public web page that uses React.

- npx is a package runner (part of npm), combination of npm install and npm start, If the package is already installed globally on your computer when you issue a command to run it with npx, the already installed package will be run. If it’s not installed, running it with npx will cause it to be downloaded, temporarily installed locally, and run.

```bash
npx create-react-app [app-name]
```

- CDN: content delivery network
- it’s possible to use React without a toolchain by including the UMD build into an HTML file
- Using react without a toolchain like create-react-app:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="app"></div>
    <script
      src="https://unpkg.com/react@latest/umd/react.development.js"
      crossorigin
    ></script>
    <script
      src="https://unpkg.com/react-­
dom@latest/umd/react-­
dom.development.js"
      crossorigin
    ></script>
    <script src="HelloWorld.js"></script>
  </body>
</html>
```

```js
"use strict";
class HelloWorld extends React.Component {
  constructor(props) {
    super(props);
    this.state = { personName: "World" };
  }
  render() {
    return React.createElement("h1", null, "Hello, " + this.state.personName);
  }
}
const domContainer = document.querySelector("#app");
ReactDOM.render(React.createElement(HelloWorld), domContainer);
```

\*\*\* some points about above code:

- The constructor will run just once, before the component is mounted. In the constructor, we use the super method to import properties from the base class (React.Component).

- The render function produces the output of every React component. React.createElement method takes three parameters:
  ➤➤The HTML element to create
  ➤➤Optional React element properties
  ➤➤The content that should be put into the created element

- React.render() creates the output of a component.

- ReactDOM.render() causes that output to be displayed in the browser window.

- Hot Reloading: files have changed and update what’s showing in the browser without you having to manually reload the page

- pull: traditional way of updating websites
- push: reactive way to build websites
- reactive programming: updating UI in response to data changes

- web apps are built in MVC pattern,
  model: data layer
  controller: facilitates communication with data layer, passes data between view and model
  view: what user sees

React only concerned with view.
React doesn't care the user is using what platform (mobile, desktop, ...)
React jus renders components

ReactDOM (libs with many funcs for interfacing between React and browser) renders React components in web browsers. (ReactDOM.render)
React Native renders React components in mobile apps.
ReactDOMDerver renders React components to static HTML.

React component (React.render()) -> Virtual DOM (ReactDOM.render()) -> DOM -> <div id="app"></div>

DOM: browser's internal representation of a web page, converts HTML, styles, and content into nodes that can be operated on using JS

when you use getElementById func or set innerHTML of an element, you interact with DOM using JS.

Compared to other kinds of JS code, DOM manipulation is slow and inefficient.

DOM’s functions: hard to use and have excessively long names like Document getElementsByClassName.

So many different JS DOM manipulation libraries have been created like jQuery that gave web developers an easy way to make updates to the DOM, and that changed the way we build UI on the web.

But jQuery's result was often inefficient UI that were slower both to download and to respond to user interactions.

When designing React, they decided to take the details of how and when the DOM is modified out of the hands of programmers. To do this, they created a layer between the code that the programmer writes and the DOM. They called this intermediary layer the Virtual DOM:

1. You write a React code to render a UI, which results in a single React element being returned.

2. ReactDOM’s render method creates a lightweight and simplified representation of the React element in memory (this is the Virtual DOM).

3. ReactDOM listens for events that require changes to the web page.

4. The ReactDOM.render method creates a new in-­memory representation of the web page.

5. The ReactDOM library compares the new Virtual DOM representation of the web page to the previous Virtual DOM representation and calculates the difference between the two. This process is called **reconciliation**.

6. ReactDOM applies just the minimal set of changes to the browser DOM in the most efficient way that it can and using the most efficient batching and timing of changes.

- React components are independent pieces that can be reused and that can pass data to each other.

- React use composition instead of inheritance by defining props for reusable components.

- Imperative programming: step by step instruction like many languages and most DOM manupilation libs

- Declarative programming: computer (or the computer language interpreter, rather) has some intelligence about the types of tasks that it can perform, and the programmer only needs to tell it what to do, rather than how to do it like React

- “idiomatic JavaScript” used to describe React. What this means is that React code is easily understandable to people who program JavaScript.

- React vs Angular vs Vue

all open-source
vue is easiest to learn, framework
react bare-bones approach
angular framework, created by google, TS necessary
vue is between has its state management, routing and managing css

- Modularization: program is organized into reusable units of code

- RequireJS: a lib to modularize JS, add this lib in script tag of HTML
  AMD (Asynchronous Module Definition) to load modules, asynchronously means all imports run prior to any of the code in that module
  define() to create module
  require() to include the module

- CommonJS (CJS): built into Node.js, modularization lib for server-side JS, load modules synchronously (parsing and executing each module as it's loaded)

\*\* Having more than one way to create and use modules made modules less reusable

- ECMAScript Modules (ESM): JS built-in standard way to modularize code, have asynchronous loading like RequireJS and simple syntax like CommonJS (using import and export)

React components are JS modules
export: creates module
default export: a default func provided by the module, only one default export per file, import default module without using {}

React components: usually default export, unless you are creating a lib of components

JSX: XML-based syntax extension to JS, not required for React component but using it is so much easier and no negative impact on performance or functionality

JSX is XML, JSX uses camelCase for HTML attributes (onclick -> onClick),
use curly braces to include literal JS,
double curly braces with objects {{}}
React with and without JSX:

```JSX
<label className="inputLabel">Search:
  <input type="text" id="searchInput"/>
</label>
```

```JS
// react without JSX
// args: element name, attributes, content, child elements
React.createElement("label", {className: "inputLabel"}, "Search:", React.createElement("input", {type: "text", id: "searchInput"}));
```

Transpiler: before run React you must build (compile) it and convert all JSX into pure JS

- Compilation vs. Transpilation

Compilation: In compiled languages (like C++ or Java), the code is converted into low-­level code (bytecode) that can be understood by the computer’s software interpreter.

Transpilation: When React applications are compiled, they’re converted from one version of JS to another version of JS.

one step in transpilation is converting JSX (not understood by browser) into plain JS

- Babel: transpilation tool, integrated into Create React App, it also eliminate browser incompatibilities with JS different versions

\*\* Prior to version 17 of React, the JSX Transform converted JSX into React.createElement() statements. With React 17, the JSX Transform was rewritten so that it transforms JSX into browser-­readable code without using
React.createElement(). The result is that developers no longer need to import
React into every component in order to use JSX.

Limited amounts of logic are necessary and perfectly normal inside of the return statement, however.
There’s no hard-­and-­fast rule for how much is too much, but, generally, any JavaScript that you write
in your JSX should only have to do with presentation, and it should be single JavaScript expressions,
rather than functions or complex logic.

- JSX elements themselves are JavaScript expressions as well, because they get converted into function calls during compilation.

- An expression is any valid unit of code that resolves to a value. Here are some JS expressions:
  ➤➤Arithmetic: 1+1
  ➤➤String: "Hello, " + "World!"
  ➤➤Logical: this !== that
  ➤➤Basic keywords and general expressions: This includes certain keywords (such as this, null,
  true, and false) as well as variable references and function calls.

\*\* use not expression statement outside of the return in React component (if, for, func)
you can use func in JSX if it is immediately invoked

return in React component can only return one thing: string, number, array, boolean, or single JSX element

React.Fragment wraps your JSX into a single JSX element, but doesn’t return any HTML.
You can use the React.Fragment component in one of three ways:

1. By using dot notation: <React.Fragment></React.Fragment>
2. By importing Fragment from the react library using curly braces
3. By using its short syntax, which is just a nameless element: < > < / >

- Component: building block of react app, a function or a JS class that optionally accepts data and returns a React element that describes some piece of the UI.

- Component vs. Element

component return an element, each compoennet within an app has unique name

element is the imported component that is used in other component Once you import a component, you can use the element it defines as many times as you need to and each usage will create a new instance of the component with its own data and memory.

SVG: Scalable Vector Graphics

React’s built-­in HTML element components have the same names as elements from HTML5. Using them in your React app causes the equivalent HTML element to be rendered.

- Attributes vs. Props

in markup langs, attributes define properties of the element: name=value

and JSX is a markup lang (XML)

props: attributes that you write in JSX element, for passing data between components, access props using component's props object

```JSX
// passing props
import Farm from './Farm';
export default function Farms(){
return(
<>
<Farm
farmer="Old McDonald"
animals={['pigs','cows','chickens']} />
<Farm
farmer="Mr. Jones"
animals={['pigs','horses','donkey','goat']} />
</>
)
}
```

```JSX
// accessing props
export default function Farm(props){
return (
<div>
<p>{props.farmer} had a farm.</p>
<p>On his farm, he had some {props.animals[0]}.</p>
<p>On his farm, he had some {props.animals[1]}.</p>
<p>On his farm, he had some {props.animals[2]}.</p>
</div>
)
}
```

\*\* when you use props inside the return statement, you have to enclose them in curly
braces.

JavaScript’s Array.map function creates a new array using the result of applying a
function to every element in an existing array. The map function is commonly used in
React to build lists of React elements or strings from arrays.
The syntax of Array.map is as follows:
array.map(function(currentValue, index, arr),thisValue)

```JSX
const bulletedList = listItems.map(function(currentItem,index){
return <li key={index}>{currentItem}</li>
}
```

➤➤ class in HTML is className in React.
➤➤ for in HTML is htmlFor in React.

**React Adds Several Attributes**

Several attributes that are available for React’s built-­in HTML components don’t exist in HTML. Chances are good that you’ll never need to use any of these special attributes, but I’m including them here for completeness. These are:

➤➤ dangerouslySetInnerHTML, which allows you to set the innerHTML property of an
element directly from React. As you can tell by the name of the attribute, this is not a recommended practice.

➤➤ suppressContentEditableWarning, which suppresses a warning that React will give you if you use the contentEditable attribute on an element that has children.

➤➤ suppressHydrationWarning. No, it’s not a way to tell React to stop nagging you to drink more water. This attribute will suppress a warning that React gives you when content generated by server-­side React and client-­side React produce different content.

**Some React Attributes Behave Differently**

Several attributes behave differently in React than they do in standard HTML:

➤➤ checked and defaultChecked. The checked attribute is used to dynamically set and unset the checked status of a radio button or checkbox. The defaultChecked attribute sets whether a radio button or checkbox is checked when the component is first mounted in
the browser.

➤➤ selected. In HTML, when you want to make an option in a dropdown be the currently selected option, you use the selected attribute. In React, you set the value attribute of the containing select element instead.

➤➤ style. React’s style attribute accepts a JavaScript object containing style properties and values, rather than CSS, which is how the style attribute in HTML works.

**Non-Standard Attributes**

In addition to the standard HTML attributes, React also supports several non-­standard attributes that have specific purposes in some browsers and meta-­data languages, including:

➤➤ autoCapitalize and autoCorrect, which are supported by Mobile Safari.

➤➤ property is used for Open Graph meta tags.

➤➤ itemProp, itemScope, itemType, itemRef, and itemID for HTML5 microdata.

➤➤ unselectable for Internet Explorer.

➤➤ results and autoSave are attributes supported by browsers built using the WebKit or Blink browser engines (including Chrome, Safari, Opera, and Edge).

- Class Components

Classes were new to JavaScript when React was first released.

React.createClass was the only way to create components but now is deprecated.

```JSX
// Creating a component with React createClass
import React from 'react';
import createClass from 'create-­react-­class';

const UserProfile = createClass({
  render() {
    return (
      <h1>User Profile</h1>
    );
  }
});
export default UserProfile;
```

Beginning with React 15.5, the preferred way of writing classes was by extending the React.Component base class directly.

```JSX
// Creating a component using a class
import React from 'react';

class UserProfile extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      <h1>User Profile</h1>
    );
  }
};
export default UserProfile;
```
