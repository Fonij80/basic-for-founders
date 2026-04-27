# ReactJS

### Interesting To Know:

- ReactJS released by facebook in 2013, UI lib for web apps
- React Native in 2015, UI lib for mobile apps

- Node.js is needed to run JS on web servers

### Node.js Tasks In Development

1. **Minification**:
   - process of removing not necessary codes (spaces, line breaks, comments) for the program to run
   - makes scripts, web pages, and stylesheets more efficient and faster

2. **Transpiling**:
   - process of converting code from one version of a programming language into another version
   - necessary because not all web browsers support the same set of new JS features, but they do all support some core subset of JS features
   - By using a JS transpiler, you can write code using the latest version of JS and then the transpiled code can be run in any web browser

3. **Module bundling**:
   - A typical website can make use of hundreds of individual JS programs. If a web browser had to download each of these programs individually, it would significantly slow down web pages due to the overhead involved with requesting files from web servers.
   - The main job of a module bundler is to combine/bundle the JS and other code involved in a web app to make serving the app faster
   - Because a bundler has to do work to all of the files in a program, it also is a good
     central place for tasks like minification and transpiling to take place, through the use of
     plugins.

[Module bundling](../../assets/module_bundling.png)

4. **Package management**:
   - managing all the JS programs (packages/libs) needed in your app

5. **CSS preprocessor**:
   - producing standard CSS from code written using an alternative syntax

   - A CSS preprocessor (like SASS or LESS) allows you to write style sheets using a superset of CSS (such as SCSS) that supports the programmatic features that CSS lacks (variables, mathematic operations, functions, scope, and nesting).

6. **Testing frameworks**

7. **Build automation**:
   - process of writing a script that runs all of the different tools for you in the right order to quickly and reliably optimize, compile, test, and deploy.

### NPM Commands

- when you install Node.js, npm will also be installed for package management.

```bash
sudo npm install -g npm  # upgrading npm

npm init -y  # create **package.json** to track dependencies

# Node.js learning resource
npm install learnyounode

or

sudo npm install learnyounode -g

learnyounode # run the package
```

### DevTools

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
import React from 'react';  // any file that defines a class component must import this lib

class UserProfile extends React.Component {

  constructor(props) {
    super(props);
    // initializing instance's state
    this.state = {
      score: 0;
      userInput: ''
    }
    // binding event handlers
    this.saveUserInput = this.saveUserInput.bind(this);
    this.updateScore = this.updateScore.bind(this);
    // where you will bind event handler functions to the instance of the class and set up the local state for the instance.
  }

  render() {
    return (
      <h1>User Profile</h1>
    );
  }
};
export default UserProfile;


or

import {Component} from 'react';

class UserProfile extends Component {

}
```

- The state of a component is stored in an object called state, and every time state changes, React attempts to re-­render the UI.

- The other object in a component instance that stores data is called **props**. This is data that is passed to a component by its parent component in a React component hierarchy. If you’re going to use the props object in the constructor, you need to pass it to the superclass’s constructor when you call super.

- By binding an event handler to the component instance, you also make it possible to share the function with other components while maintaining its link to the state of the instance with which it’s bound. The result is that no matter where the event handler is, it always uses and affects the data from its bound object.

```JSX
// Not binding your functions results in errors

// this.handleClick is passed as a variable and becomes an ordinary function without an owner object. When the click event happens inside the button component, this falls back to referring to the global object, and we get an error because this.message doesn’t exist

import React from 'react';

class Foo extends React.Component{
  constructor( props ){
    super( props );
    this.message = "hello";
  }

  handleClick(event){
    console.log(this.message); // 'this' is undefined
  }

  render(){
    return (
      <button type="button" onClick={this.handleClick}>
        Click Me
      </button>
    );
  }
}

export default Foo;
```

```JSX
// Binding a function and using it in another class

// you can pass handleClick as a prop to other components and it will always run within the context of Foo

import React from 'react';

class Foo extends React.Component{

  constructor( props ){
    super( props );
    this.message = "hello";
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick(event){
    console.log(this.message); // 'hello'
  }

  render(){
    return (
      <button type="button" onClick={this.handleClick}>
        Click Me
      </button>
    );
  }
}

export default Foo;
```

- JS Classes

- traditional classes = bluprints for object creation

- JS classes are obj themselves that serve as a template for objects. Js has prototypes, not true classes.

\*\* Syntactic sugar (introduced in ES2015) refers to a simplified or abstracted way of writing something that makes it easier to write or to understand, but doesn’t actually do anything that you couldn’t previously do like class syntax (no new functionality, just a new syntax which is more familiar to oop programmers for creating class)

- class syntax in JS is a new way to use function constructors and prototypal inheritance.

- Prototypal Inheritance
  JavaScript objects are collections of properties. In prototypal inheritance, every object inherits properties and methods from its prototype object. JavaScript has several ways to create objects:

1. By using Object Literal notation.
2. By using the Object.create method.
3. By using the new operator: write a constructor function and invoke it by _new_

- built-­in _Object_ object is the prototype for every JavaScript object.

- A property with a function value is what we refer to as a “method” in JavaScript.

```JS
// a is the prototype for b
let a = function () {
  this.x = 10;
  this.y = 8;
};
let b = new a();

a.prototype.z = 100 // add new properties

a.prototype.sum = function() { return this.x + this.y }; // add function property (method)

b.sum() // 18
```

\*\* every object that you create in JavaScript is a copy of another
object, which is called its prototype. Objects inherit properties and values from their prototype and have a link back to their prototype. If a property is referenced on an object and that object doesn’t contain that property, JavaScript will look at the object’s prototype and so on up the chain of prototypes until it gets to the built-­in Object.

\*\* An important difference between class declarations and function declarations, however, is that function declarations are hoisted. Function hoisting means that you can reference a function created using a function declaration anywhere in a script, even before the function declaration actually appears in the file.

- default constructor = empty function

```JS
// class declaration, can't be hoisted (use it before its declaration)
class Pizza {
  constructor(toppings,size) {
    this.toppings = toppings;
    this.size = size;
  }
}

// named class expression
let Pizza = class Pizza {
  constructor(toppings,size) {
    this.toppings = toppings;
    this.size = size;
  }
}

// when using class expression with a named class, the name after class keyword is accessible by name property
console.log(Pizza.name); // Output: "MyPizza"
// unnamed class declaration
let Pizza = class {
  constructor(toppings, size) {
    this.toppings = toppings;
    this.size = size;
  }
};

// function decalration

let MyPizza = new Pizza(['sausage','cheese'],'large'); // hoisting function (calling it before its declaration)

function Pizza(toppings,size) {
  this.toppings = toppings;
  this.size = size;
}
```

\*\* In functional programming, programs are created by applying and composing functions, and functions are “first-­class citizens.” What this means is that JavaScript functions are treated like any other variable. They can be passed as values into other functions, they can return other functions, and they can be assigned as a value to a variable.

- What is _this_ in a function?

- By default, when you use the this keyword inside a function and then invoke that function, this gets set to the global object, which in a web browser is the window object. but in "strict" mode, this will be set to _undefined_.

```JS
function sum(a,b) {
  this.secretNumber = 100;
  return a+b;
}

let mySum = sum(2,5);
console.log(window.secretNumber); // 100


function getSecretNumber(){
  'use strict';
  this.secretNumber = 100;
  return this.secretNumber;
}

console.log(getSecretNumber()); // error: cannot set property 'secretNumber' of undefined.
```

- Strict Mode:
  More often than not, when you add properties to the global object, it’s a mistake. Strict mode makes this mistake have immediate consequences, rather than letting your code appear to work correctly while containing potentially dangerous global variables.

```JS
// method syntax with function()
const author = {
  write: function() {
    return 'Writing!';
  }
}
let status = author.write();

// method syntax without function
const author = {
  write() {
    return 'Writing!';
  }
}

// function bunding
const author1 = {
  totalWords: 0
}
const author2 = {
  totalWords: 0
}

const write = function(words) {
  this.totalWords += words;
  return this.totalWords;
}

// binds a function with an object and invokes the function, pass the obj's name and needed args
write.call(author1,500);

// binds a function with an object and invokes the function, pass the obj's name and needed args in array format
write.apply(author1,[500]);

// returns a new function that’s bound to the specified object, second arg is optional
let write500Words = write.bind(author1,500);
write500Words();
```

\*\* Function binding is important in React components, because it allows you to define a function in one component and then pass it as a variable into other components, while still operating on the component where the function was initially defined.

### State Management in Class Component

- The constructor function is the only place where you should ever directly update the state object of a component. For updating the state after the constructor function has run (during the life of the component), React provides a function called _setState_.

- _setState_ is asynchronous, means f you try to access state immediately after setting it, you may get the old value rather than the new value that you expect. changes to state may be batcjed for performance reasons.

### State Management in Function Component

- each time a JS func runs, its vars are initialized so a func component can't have persistent local vars.

- Hook: a func that let you "hook" into functionality of class components without writing a class

- _useState_: a hook that lets you persist data with functional component, returns an array (contains a stateful var) and a func (for updating that var)

### Functions vs Classes

| Function component | Class Component |
| Accepts props as arguments and returns a React element | Extends React.Component|
| No render method | Requires a render method |
No internal state (can be simulated using hooks) | Has internal state |
Can use hooks | Cannot use hooks |
Cannot use lifecycle methods (can be simulated using hooks) | Can use lifecycle methods |

### Parent and Children

- By using this.props.children (or props.children in the case of function components) in the return statement of a component, you can create components where the child components aren’t known until the component is invoked. it's descriptor of the children not the actual children.

React provides several built-­in ways to access information about and manipulate elements. These are:

➤➤ isValidElement: takes an object as an argument and returns either true or false
depending on whether the object is a React element.

➤➤ cloneElement: The cloneElement function creates a copy of an element passed into it. With cloneElement, you can create new elements from a component’s child elements, and modify
them in the process.

- const NewElement = React.cloneElement(element,[props],[children]);

➤➤ React.Children

React.Children provides several utility functions that operate on the children of a component. For each of these, you can pass in props.children as an argument. These utilities are:

➤➤ React.Children.map. Invokes a function for each immediate child element and returns a new array of elements.

➤➤ React.Children.forEach. Invokes a function for each immediate child but doesn’t return anything.

➤➤ React.Children.count. Returns the number of components in children.

➤➤ React.Children.only. Verifies that children only has one child.

➤➤ React.Children.toArray. Converts children to an array.

```JSX
// Using state and setState in a class component
import {Component} from 'react';

class Counter extends Component {

  constructor(props) {
    super(props);
    this.state = {count: 0};
    this.incrementCount = this.incrementCount.bind(this);
  }

  incrementCount() {
    this.setState({count: this.state.count + 1});
  }

  render() {
    return (
      <div>
        <p>The current count is: {this.state.count}.</p>
        <button onClick = {()=>{this.incrementCount(this.state.count+1)}}>
          Add 1
        </button>
      </div>
    );
  }
}

export default Counter;
```

### Render Function

- only required function in class-based component. It runs when the component mounts and updates.

- return statement can only return one element/array/string.

### Props

- args that you pass into a component from a parent component

- In JSX, attrs (name=value) become properties inside the _props_ object.

```JSX
// Using props to pass data to a child component
import {Component} from 'react';
import BasicFigure from './BasicFigure';

class FigureList extends Component {
  render() {
    return (
      <div style={{display:"flex"}}>
        <BasicFigure filename="dog.jpg" caption="Chauncey" />
        <BasicFigure filename="cat.jpg" caption="Murray" />
        <BasicFigure filename="chickens.jpg" caption="Lefty and Ginger" />
      </div>
    )
  }
}

export default FigureList;


// Using props in a class component
import {Component} from 'react';

class BasicFigure extends Component {
  render() {
    return(
      <figure>
        <img src={this.props.filename} alt={this.props.caption}/>
        <figcaption>{this.props.caption}</figcaption>
      </figure>
    );
  }
}

export default BasicFigure;
```

### Function Components

- much easier than class components

- JS functions that return React element

- at first they were just used for stateless functional component = dumb component = presentational component, no internal state data or operations like fetching and posting

- then _Hooks_ were introduced in React 16.8, allow function component to interacting with data store and using state

```JSX
// function component with function declaration
function Foo(props){
  return <h1>Welcome</h1>;
}
export default Foo;

// function component with function expression
const Foo = function(props){
  return <h1>Welcome</h1>;
}
export default Foo;

// function component with arrow fucntion
const Foo = (props) => {
  return <h1>Welcome</h1>;
}
export default Foo;
```

### Arrow function's rules

1. The parentheses around the parameter list are optional when a function only takes one parameter.

2. The return keyword is optional when an arrow function doesn’t do anything except return data.

3. The curly braces around the function body are optional if you skip the return keyword.

### JS vars

- from ES2015, 2 new keyword added: const, let

- JavaScript evaluates declarations first within their scope through a process called hoisting. When you use the var keyword to declare a variable, JavaScript also initializes the variable with a value of undefined during the hoisting. What this means in practice is that it’s possible to use a variable created with var before it’s declared

- Variables created using var have function scope. What this means is that if you declare a variable inside a function, you can use that variable anywhere in the function.

- If you declare a variable outside of a function, it will have global scope, meaning that you can use it anywhere in your program.

\*\* In reality, if a global is what you want (and if you’re not using “strict” mode) you didn’t even need to use the var keyword, because if you just assigned a value to a name, the result will be a global variable, no matter where in your program you do the assignment. Another way to think about what happens when you create a variable without declaring it is that a new property is created on the global object (window in the case of a browser). This “feature” of loose-­mode JavaScript is called implicit globals, and it can be very dangerous, which is why strict mode disallows it.

#### Const

- block scope vars

- The const keyword creates a variable that can only have one value during its
  lifetime, which we call a constant. To create a constant, just use the const keyword followed by a valid name:
  const x;
  However, because you can’t change a constant, and because declaring a vari‑
  able automatically assigns it a value of undefined, if you want your constant to
  have a value other than undefined, you must initialize it at the same time as the declaration:
  const x = 10;
  Attempting to change the value of a const will result in an error in JavaScript. Note, however, that if you assign an object or an array to a constant, you can still change the properties of that object or the items in the array. You would not be able to reassign the variable with a completely new object or array, however.

#### Let

- creates a block-scoped var (lexical var scoping)

- Destructuring Assignment
  Destructuring assignment syntax lets you create variables by unpacking the elements
  in an array or the properties of an object. For example, say you have the follow‑
  ing object:
  const User = {
  firstName: 'Lesley',
  lastName: 'Altenwerth',
  userName: 'roosevelt86',
  address: '81592 Daniel Underpass',
  city: 'Haileeshire',
  birthday: '1963-­
  10-­
  12'
  }
  If you want to create individual variables from the properties in this object, one way
  to do it is to declare and assign individual variables, like this:
  const firstName = User.firstName;
  const lastName = User.lastName;
  const userName = User.userName;
  ...
  Using destructuring syntax, you can do it all in one statement:
  const {firstName,lastName,userName,address,city,birthday} = User;
  To use destructuring with arrays, use square brackets:
  const [firstName,lastName] = ['Lesley','Altenwerth'];

```JS
x = 10;
console.log(x);
var x;

// same as
var x;
x = 10;
console.log(x);

// same as
var x=10;
console.log(x);
```

```JSX
export const Foo = props => <h1>Hello, World!</h1>;
```

```JSX
// class component
import React from 'react';

class ToDoClass extends React.Component {

  constructor(props) {
    super(props);
    this.state = {
      item: '',
      todolist: []
    }
    this.handleSubmit = this.handleSubmit.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }

  handleSubmit(e){
    e.preventDefault();
    const list = [...this.state.todolist, this.state.item];
    this.setState({
      todolist:list
    })
  }

  handleChange(e){
    this.setState({item:e.target.value});
  }

  render() {
    const currentTodos = this.state.todolist.map(
    (todo,index)=><p key={index}>{todo}</p>);

    return (
      <form onSubmit={this.handleSubmit}>
        <input type="text"
          id="todoitem"
          value={this.state.item}
          onChange={this.handleChange}
          placeholder="what to do?" />
        <button type="submit">
          Add
        </button>
          {currentTodos}
      </form>
    );
  }
}

export default ToDoClass;

// function component
import {useState} from 'react';

export const ToDoFunction = (props)=> {

  const [item,setItem] = useState('');
  const [todolist,setTodoList] = useState();

  const handleSubmit = (e)=> {
    e.preventDefault();
    const list = [...todolist, item];
    setTodoList(list)
  }

  const currentTodos = todolist.map((todo,index)=><p key={index}>{todo}</p>);

  return (
    <form onSubmit={handleSubmit}>
      <input type="text"
        id="todoitem"
        value={item}
        onChange={(e)=>{setItem(e.target.value)}}
        placeholder="what to do?" />
      <button type="submit">
        Add
      </button>
        {currentTodos}
    </form>
  );
}

// using named export for function component import instead of default
import {ToDoFunction} from './ToDoFunction';
```

### Component Lifecycle

- At each stage in the life of a component, certain events are fired and methods are invoked. These events and methods make up the component lifecycle.

1. Mounting: from component construction to insertion into DOM, rendering JSX returned by component, below methods run:
1. constructor(): initialization of the component’s state object, and binding of event handlers

1. static getDerivedStateFromProps: to check whether the props that the component uses have changed and to use the new props to update the state. This method runs both during the mounting stage as well as during the updating stage.

1. render: runs once during the mounting stage, After mounting, render runs every time the component updates. This is the method that generates the JSX output of your component, and it’s the only required method in a class component.

1. componentDidMount(): uns when the component has finished mounting and has been inserted in the browser DOM. This is the point at which it’s safe to do things that depend on DOM nodes, or to fetch remote data.

1. Updating: when the state of the component changes and the component is re-rendered

1. shouldComponentUpdate: If you have a component that you know will never need to be updated once it’s mounted, you can prevent it from updating by using this code:

```JSX
  shouldComponentUpdate() {
    return false;
  }

  // Comparing previous and next props in shouldComponentUpdate
  class ToDoItem extends Component {

    shouldComponentUpdate(nextProps, nextState) {
      return nextProps.isChecked != this.props.isChecked;
    }
  }
```

2. getSnapshotBeforeUpdate: happens right before the rendered output from the component is made active in the DOM, allow you to capture information about the state of the browser (or other output device) prior to it changing,

one example use for it is to maintain the scroll position of an element (such as a text box) between renders. If an update to the browser DOM would affect what the user is currently viewing in the browser, getSnapshotBeforeUpdate can be used to find out the relevant information about the browser DOM so that it can be restored after the update happens.

3. componentDidUpdate: runs immediately after a component updates, useful for performing network requests based on new props passed to the component, or for performing operations that depend on the snapshot of the DOM created during the getSnapShotBeforeUpdate method

4. Unmounting: removing a component from the DOM (end of lifecycle)

5. componentWillUnmount: invoked right before a component is removed from the DOM. If you need to do any cleanup in your application related to the component that will be unmounted, this is the place to do it like Stopping any network requests that are in progress, Stopping timers, Removing event listeners created in componentDidMount

6. Error handling: these methods run when an error happens during component lifecycle

- In class components, you can override the lifecycle methods to run your own code in response to lifecycle events. Function components can simulate lifecycle methods using a hook called useEffect

## Data Flow

### One-way data flow (unidirectional)

- all data flow from parent component to child

- \*\*Data flows down (downstream by using props), events flow up (upstream by usestate hook).\*\*

- one-­way data flow does mean that the way you send data from a child component to a parent component or between sibling components is different from how you pass data from a parent to a child.

- Two-­way data flow (bidirectional): where a component’s data can be modified by its parent and changes within the component can directly affect data in the parent, not possible to tell whether the view was updated by the user interacting with the view or by the data in the model changing

### Props

- primary way to share data between components, read-only (immutable), of any types:
  - primitive: undefined, Boolean, Number, String, BigInt, Symbol
  - object
  - function
  - array
  - null

- Changing local variables and props inside the component doesn’t update the view -> you must change the state

```JSX
<Taco meat="chicken" produce={[cabbage,radish,cilantro]} sauce="hot" />
// above component props like below function call
Taco({meat:"chicken",produce:[cabbage,radish,cilantro],sauce:"hot"});
```

#### PropTypes

- a tool for type checking and documenting props in React components: validating data type, required props, nodes

- a missing prop won’t trigger a PropType warning message by default

- each prop will be tested by a rule -> fail test -> console warning in development mode, no compilation error

- Node: anything that can be rendered in a component like number, string, element, arrays containing number, string, element

```bash
npm install prop-­types -­-­save
```

```JSX
import PropTypes from 'prop-­
types';

function MyComponent(props) {
  return (<p>The value is {props.itemValue}</p>);
}

MyComponent.propTypes = {
  itemValue: PropTypes.number,
  itemValueRequired: PropTypes.string.isRequired,
  itemNode: PropTypes.node,  // checks whether its value can be rendered
  children: PropTypes.element.isRequired,  // checks whether the prop contains a rendered element (<Element />)
  itemType: PropTypes.elementType,  // checks whether the prop contains a unrendered element (Element)
}

export default MyComponent;
```

```JSX
// Validating that a prop is an instance of a class
import {Component} from 'react';
import {PropTypes} from 'prop-­
types';
import Person from './Person';

class FamilyTree extends Component {
  render() {
    return (
      <p>{this.props.father.firstName}</p>
    )
  }
}

FamilyTree.propTypes = {
  father: PropTypes.instanceOf(Person)
}

export default FamilyTree;
```

```JSX
// check whether the value of a prop is one of the specific items in a list
import PropTypes from 'prop-­
types';

function DisplayPrimaryColor(props) {
  return(
    <p>You picked: {props.primaryColor}</p>
  )
}

DisplayPrimaryColor.propTypes = {
  primaryColor:PropTypes.oneOf(['red','yellow','blue'])
}

export default DisplayPrimaryColor;

// check whether the value of a prop is one of a list of data types
Component.propTypes = {
  myProp:PropTypes.oneOfType([
    PropTypes.bool,
    PropTypes.string,
    PropTypes.number
  ])
}

// tests that the prop is an array in which each of the elements matches a provided type
MyComponent.propTypes = {
  students: PropType.arrayOf(
    PropTypes.instanceOf(Person)
  )
}

// tests that the prop is an object in which each of the properties of the object match a provided type
MyComponent.propTypes = {
  scores: PropTypes.objectOf(
    PropTypes.number
  )
}

// tests whether a prop value is an object containing specific properties
MyComponent.propTypes = {
  userData: PropTypes.shape({
    id: PropTypes.number,
    fullname: PropTypes.string,
    birthdate: PropTypes.instanceOf(Date),
    isAdmin: PropTypes.bool
  })
}

// performs a strict object match on the prop, meaning that it must include only the specified properties, each of which must pass its validation
MyComponent.propTypes = {
  toDoItem: PropTypes.exact({
    description: PropTypes.string,
    isFinished: PropTypes.bool
  })
}
```

#### Creating Custom PropTypes

```JSX
// Using a custom validator to test for a phone number
import PropTypes from 'prop-­
types';

function Contact(props) {
  return(
    <li>{props.fullName}: {props.phone}</li>
  )
}

const isPhoneNumber = function(props, propName, componentName) {
  const regex = /^(\+\d{1,2}\s)?\(?\d{3}\)?[\s.-­]\d{3}[\s.-­]\d{4}$/;

  if (!regex.test(props[propName])) {
    return new Error(`Invalid prop ${propName} passed to ${componentName}.
    Expected a phone number.`);
  }
}

Contact.propTypes = {
  fullName: PropTypes.string,
  phone: isPhoneNumber,
}

export default Contact;
```
